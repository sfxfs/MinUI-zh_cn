# Repository Guidelines

## Project Overview

MinUI is a minimalist custom launcher and libretro frontend for retro gaming handhelds, written in C99. It supports 12+ platforms (Miyoo Mini, RG35XX, TrimUI Smart, TG5040, RGB30, etc.) from a single SD card. Two main executables: **minui** (the launcher/file browser) and **minarch** (the libretro frontend that loads emulator cores via `dlopen`).

## Architecture & Data Flow

Three-layer platform abstraction:

1. **Platform HAL** (`workspace/<platform>/`) — Each device implements ~30 `PLAT_*` functions (video, input, battery, power, rumble) in `platform.c`/`platform.h`, plus a `keymon` daemon (hardware button combos, battery monitoring) and `libmsettings` (shared memory IPC for brightness/volume/jack).
2. **Common API** (`workspace/all/common/`) — Platform-independent subsystems: `GFX_*` (SDL rendering, sprite atlas UI, scalers), `PAD_*` (bitmask input with repeat), `PWR_*` (sleep/wake/autosleep), `SND_*` (audio), `VIB_*` (rumble). Declared in `api.h`, implemented in `api.c`.
3. **Applications** (`workspace/all/`) — `minui` (launcher), `minarch` (libretro frontend), plus utilities (`clock`, `minput`, `say`, `syncsettings`).

**Runtime flow**: Boot → `updater` detects platform via `/proc/cpuinfo` → platform `boot.sh` → `launch.sh` starts daemons (keymon, batmon, etc.) → runs `minui.elf` in a loop. When user selects a ROM, minui writes a command to `/tmp/next` and exits; `launch.sh` evals it (launching `minarch.elf <core.so> <rom>`), then loops back to minui.

**PAK system**: Emulators/tools are `.pak` directories containing `launch.sh` and optional `default.cfg`. See `PAKS.md`.

## Key Directories

| Directory | Purpose |
|---|---|
| `workspace/all/common/` | Shared C library: `api.c/h`, `defines.h`, `utils.c/h`, `scaler.c/h`, `sdl.h` |
| `workspace/all/minui/` | Launcher application (`minui.c`, ~1700 lines) |
| `workspace/all/minarch/` | Libretro frontend (`minarch.c`, ~4800 lines) |
| `workspace/all/{clock,minput,say,syncsettings}/` | Small utility tools |
| `workspace/all/cores/` | Shared libretro core build template (`makefile`) |
| `workspace/<platform>/platform/` | Per-device HAL: `platform.c`, `platform.h`, `makefile.env`, `makefile.copy` |
| `workspace/<platform>/keymon/` | Per-device key monitoring daemon |
| `workspace/<platform>/libmsettings/` | Per-device shared settings library (POSIX shm IPC) |
| `workspace/<platform>/cores/` | Per-device libretro core definitions and patches |
| `workspace/<platform>/show/` | Per-device splash screen utility |
| `workspace/<platform>/install/` | Per-device boot/install scripts |
| `skeleton/` | SD card layout template (BOOT, BASE, SYSTEM, EXTRAS) |
| `skeleton/SYSTEM/<platform>/paks/` | Per-platform emulator/tool pak definitions |

## Development Commands

### Build (runs on host, macOS/Linux)

```sh
# Build all platforms and package release
make

# Build a single platform
make miyoomini
make rg35xxplus

# Open interactive Docker shell for a platform
make PLATFORM=miyoomini shell

# Inside Docker: build just the workspace
make build

# Build specific targets inside Docker
make common    # build + system + cores
make system    # copy binaries to skeleton
make cores     # copy libretro cores to skeleton
```

### Build order (inside Docker, per `workspace/makefile`)

libmsettings → platform `early` (third-party deps) → keymon → minui → minarch → clock → minput → syncsettings → say → platform cores → platform `all`

### Packaging

```sh
make package   # Creates MinUI-YYYYMMDD-N-base.zip and -extras.zip in releases/
```

### Toolchain setup

Toolchains are Docker images built from `github.com/shauninman/union-<PLATFORM>-toolchain`. Cloned automatically on first use into `toolchains/`. Each platform has its own cross-compiler and sysroot.

## Code Conventions & Common Patterns

### Language & compilation

- **C99** (`-std=gnu99`), compiled with `-Ofast`
- SDL1.2 or SDL2 depending on platform (controlled by `USE_SDL2` define in `makefile.env`)
- ARM NEON SIMD used in scalers where available (`HAS_NEON` in `platform.h`)

### Naming

- **Types/structs**: `PascalCase` — `GFX_Renderer`, `PAD_Context`, `Option`
- **Functions**: `PREFIX_camelCase` — `GFX_blitPill()`, `PAD_justPressed()`, `PLAT_initVideo()`
- **Macros/constants/enums**: `UPPER_SNAKE_CASE` — `BTN_DPAD_UP`, `FIXED_WIDTH`, `MAX_PATH`
- **Prefixes**: `GFX_` (graphics), `PAD_` (input), `PWR_` (power), `SND_` (sound), `VIB_` (rumble), `PLAT_` (platform HAL), `BTN_` (button bitmask), `LOG_` (logging)

### Platform abstraction pattern

No `#ifdef PLATFORM_X` in common code. Each platform is compiled separately in its own Docker toolchain. Common code uses `PLAT_*` function declarations in `api.h`; platforms provide implementations. Default implementations use `__attribute__((weak))` via `FALLBACK_IMPLEMENTATION` macro — platforms override only what they need.

### Module state

Static structs for module-scoped state:
```c
static struct GFX_Context { ... } gfx;
static struct PWR_Context { ... } pwr = {0};
```

### Memory management

- `malloc`/`calloc`/`realloc`/`free` with caller-must-free convention
- `allocFile()` returns heap-allocated content the caller must free
- Settings use POSIX `shm_open`/`mmap` for zero-copy IPC between keymon and applications
- `Array` and `Hash` structs (in minui.c) manage their own memory with explicit `_free` destructors

### String handling

- `strcpy`/`sprintf`/`strcat` with `MAX_PATH 512` buffers (no bounds checking in most places)
- Case-insensitive matching via `strncasecmp`/`strcasestr` in `utils.c`

### Include guards

```c
#ifndef __NAME_H__
#define __NAME_H__
// ...
#endif
```

### Comments

- `//` inline comments, `////////////////` section dividers
- `// buh` for intentional no-op stubs
- `// TODO:` markers for known issues

### Indentation

Tabs for code, spaces for alignment within struct initializers and macro definitions.

### Error handling

Minimal — file ops check return values (`fopen` NULL, `fd < 0`), log on failure, most functions return void.

### SDL abstraction

`sdl.h` wraps SDL1.2 vs SDL2 behind `USE_SDL2` define. Provides `SDLX_SetAlpha` compatibility macro. Platforms set `SDL=SDL2` in `makefile.env` to opt into SDL2.

## Important Files

| File | Role |
|---|---|
| `workspace/all/common/api.h` | Central API: all GFX/PAD/PWR/SND/VIB/PLAT declarations |
| `workspace/all/common/api.c` | Core API implementation (~1700 lines) |
| `workspace/all/common/defines.h` | Path templates, colors, UI layout, button enums |
| `workspace/all/common/scaler.c` | ARM NEON and C integer pixel scalers (1x-6x) |
| `workspace/all/common/utils.c` | String matching, ROM name extraction, file I/O |
| `workspace/all/common/sdl.h` | SDL1.2/SDL2 compatibility layer |
| `workspace/all/minui/minui.c` | Launcher: directory browser, ROM listing, game launch |
| `workspace/all/minarch/minarch.c` | Libretro frontend: core loading, video pipeline, save states, in-game menu |
| `workspace/<platform>/platform/platform.h` | Per-device constants: screen size, button mappings, features |
| `workspace/<platform>/platform/platform.c` | Per-device HAL implementation |
| `workspace/<platform>/platform/makefile.env` | Per-device compiler flags, SDL version, libraries |
| `workspace/<platform>/libmsettings/msettings.h` | Shared settings API (identical across platforms) |
| `workspace/<platform>/keymon/keymon.c` | Per-device key daemon |
| `PAKS.md` | PAK system documentation |
| `skeleton/SYSTEM/<platform>/system.cfg` | Per-platform minarch option locks |

## Runtime/Tooling Preferences

- **Build host**: macOS or Linux (root makefile runs on host)
- **Cross-compilation**: Docker containers with per-platform toolchains (ARM: Cortex-A7, A9, A53, A55 variants)
- **No CI/CD**: Builds are local only. The only GitHub Action auto-closes PRs.
- **No PRs accepted**: Solo developer project by @shauninman
- **Release process**: Manual `make` + `make package`, creates dated zip files
- **Platform toolchains**: `github.com/shauninman/union-<PLATFORM>-toolchain` repos, cloned into `toolchains/`

## Testing & QA

No automated test suite. Verification is manual on hardware. A `workspace/macos/platform/` exists for native macOS compilation to catch build errors without Docker round-trips. The `todo.txt` file serves as the active development log with device-specific issues and investigations.

## Platform Families

| Family | Platforms | SDL | Notes |
|---|---|---|---|
| Miyoo | miyoomini, my355, my282 | SDL1/SDL2 | SigmaStar SoC, MI_GFX hardware blitter on miyoomini |
| TrimUI | trimuismart, tg5040 | SDL1/SDL2 | sunxi display, ION memory on trimuismart |
| Anbernic | rg35xx, rg35xxplus, rgb30 | SDL1/SDL2 | rg35xxplus supports HDMI, external gamepads, device variants |
| Others | m17, gkdpixel, zero28, magicmini | SDL1/SDL2 | Varying feature sets |
