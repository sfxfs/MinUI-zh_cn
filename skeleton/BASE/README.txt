MinUI 是一个极简启动器，支持 Trimui Smart（及 Pro）和 Brick、Miyoo Mini（及 Plus）、A30 和 Flip、Powkiddy RGB30、M17、MagicX XU Mini M 和 Mini Zero 28，以及 Anbernic RG*XX 系列——全部来自同一张 SD 卡。为什么？何乐而不为呢？

源码：
https://github.com/shauninman/minui

----------------------------------------
安装

前言

MinUI 有两个基本部分：一个名为 "MinUI.zip" 的安装/更新 zip 压缩包，以及一个引导文件或文件夹（名称因平台而异）。

在支持双 SD 卡的设备上（如 RG35XX），我将使用 "TF1" 来指代插入设备第一个插槽的卡。所有其他提到的 "SD 卡" 或 "主卡" 指的是插入第二个插槽的卡，或仅支持单卡设备的唯一 SD 卡。为了能够在多台设备上使用单张 SD 卡运行 MinUI，你必须将其安装在支持双 SD 卡设备的第二张卡上。

主卡应为知名品牌，并格式化为 FAT32（MBR）。

注意事项

虽然 MinUI 安装后可以从任何设备更新，但某些设备需要对 NAND 或 TF1 进行（轻微的）更改（通过上述引导文件或文件夹），因此需要在使用前从特定设备安装。在同类新设备上使用现有卡时也是如此。如有疑问，请按照安装说明操作；如果所有必要的组件已安装，安装程序将仅充当更新程序。

通用步骤

预加载 "Bios" 和 "Roms" 文件夹，然后将两者复制到主卡的根目录。

RGB30

MinUI 需要与安装在左侧插槽（标记为 TF-OS）SD 卡上的 Moss 配合使用。下载并刷入最新版本：

	https://github.com/shauninman/Moss/releases

将 "MinUI.zip"（无需解压）复制到插入右侧插槽（标记为 TFGAME）的 SD 卡根目录。

MAGICX XU MINI M

MinUI 需要与安装在左侧插槽（标记为 TF1/INT）SD 卡上的深度修改版原厂固件配合使用。下载并刷入最新版本：

	https://github.com/shauninman/Moss-magicmini/releases

将 "MinUI.zip"（无需解压）复制到插入右侧插槽（标记为 TF2/EXT）的 SD 卡根目录。

MAGICX MINI ZERO 28

MinUI 需要与安装在左侧插槽（标记为 TF1/INT）SD 卡上的 Moss 配合使用。下载并刷入最新版本：

	https://github.com/shauninman/Moss-zero28/releases

将 "magicx" 文件夹和 "MinUI.zip"（无需解压）复制到插入右侧插槽（标记为 TF2/EXT）的 SD 卡根目录。

TRIMUI SMART / TRIMUI SMART PRO / TRIMUI BRICK

将 "trimui" 文件夹和 "MinUI.zip"（无需解压）复制到 SD 卡根目录。

MIYOO MINI / MIYOO A30

将 "miyoo" 文件夹和 "MinUI.zip"（无需解压）复制到 SD 卡根目录。

MIYOO MINI PLUS

将 "miyoo354" 文件夹和 "MinUI.zip"（无需解压）复制到 SD 卡根目录。

如果你的设备有可用的 RTC，可以通过在 "/.userdata/miyoomini/" 中创建一个名为 "enable-rtc"（无扩展名）的空文件来启用它。

MIYOO FLIP

将 "miyoo355" 文件夹和 "MinUI.zip"（无需解压）复制到 SD 卡根目录。将 SD 卡插入右侧插槽（电源按钮下方）。

MIYOO MINI FLIP

将 "miyoo285" 文件夹和 "MinUI.zip"（无需解压）复制到 SD 卡根目录。

M17

将 "em_ui.sh" 文件和 "MinUI.zip"（无需解压）复制到 SD 卡根目录。

RG35XX PLUS / RG35XX H / RG35XX 2024 / RG28XX / RG35XXSP / RG40XXH / RGCUBEXX / RG34XX / RG34XXSP

MinUI 需要安装在全新的原厂 Anbernic 固件上。你可以使用原厂 TF1 卡，关于其质量差的传言被大大夸大了，而且只要你使用推荐的双卡设置，它上面不会存储任何用户数据。（注意：PLUS/H/2024/SP 的原厂 TF1 与 28XX/40XXH 不兼容，反之亦然。）

将 "/rg35xxplus/dmenu.bin"（仅文件）复制到 TF1 卡的 "NO NAME" 分区（带有 "anbernic" 文件夹的 FAT32 分区）根目录。将 "MinUI.zip"（无需解压）复制到 TF2 卡根目录。

GKD PIXEL / GKD MINI

重要提示：此设备与其他 MinUI 支持的设备不兼容，因为其固件存储在 SD 卡上，其存在会干扰所有其他设备。

备份你的原厂 SD 卡（不仅仅是 "ROMS" 分区，而是整张卡）。如果你喜欢冒险，只需在 "ROMS" 分区上创建一个名为 "stock" 的文件夹，并将所有内容复制到该文件夹中。

将 "gkdpixel" 文件夹和 "MinUI.zip"（无需解压）复制到 SD 卡的 "ROMS" 分区根目录。（GKD Mini 应为 TF1。）

启动原厂系统，导航到 "APP" 文件夹并启动 "file manager"。然后使用方向键和 A 按钮导航到 "/media/roms/gkdpixel"。选中 "install.sh" 文件并按 A 打开菜单，选择 "Execute" 来安装 MinUI。

RG35XX（初代）

MinUI 需要安装在全新的原厂 Anbernic 固件上。你可以使用原厂 TF1 卡，关于其质量差的传言被大大夸大了，而且只要你使用推荐的双卡设置，它上面不会存储任何用户数据。

将 "/rg35xx/dmenu.bin"（仅文件）复制到 TF1 卡的 MISC 分区根目录。将 "MinUI.zip"（无需解压）复制到 TF2 卡根目录。

----------------------------------------
更新

通用步骤

将 "MinUI.zip"（无需解压）复制到包含你的 ROM 的 SD 卡根目录。

----------------------------------------
快捷键

对于没有专用 MENU 按钮的设备

	RGB30：使用 L3 或 R3 作为 MENU
	M17：  使用 + 或 - 作为 MENU

RGB30 / MIYOO MINI PLUS / RG35XX (PLUS) / TRIMUI SMART PRO / TRIMUI BRICK / GKD PIXEL / MIYOO A30 / MAGICX XU MINI M / MIYOO FLIP / MAGICX MINI ZERO 28
  
  亮度：MENU + 音量增大
           或 音量减小
  
MIYOO MINI / TRIMUI SMART / M17

  音量：SELECT + L 或 R
  亮度：START + L 或 R

RGB30 / MIYOO MINI (PLUS) / RG35XX (PLUS) / TRIMUI SMART PRO / TRIMUI BRICK / GKD PIXEL / MIYOO A30 / MAGICX XU MINI M / MIYOO FLIP / MAGICX MINI ZERO 28
  
  休眠：POWER
  唤醒：POWER
  
TRIMUI SMART / M17
  
  休眠：MENU（按两次）
  唤醒：MENU

TRIMUI SMART PRO / TRIMUI BRICK

  静音：FN 开关（音量和振动）

----------------------------------------
快速存档与自动恢复

MinUI 会在游戏中关机时创建快速存档。下次开机时，它将自动从你离开的地方恢复。快速存档在手动关机或短暂停眠后自动关机时创建。在没有 POWER 按钮的设备上（如 Trimui Smart 或 M17），在拨动电源开关之前按两次 MENU 按钮使设备休眠。

----------------------------------------
ROM

此压缩包中包含一个 "Roms" 文件夹，其中包含 MinUI 当前支持的每个主机的文件夹。你可以重命名这些文件夹，但必须保留括号中的大写标签名称，以保持与正确模拟器的映射（例如，"Nintendo Entertainment System (FC)" 可以重命名为 "Nintendo (FC)"、"NES (FC)" 或 "Famicom (FC)"）。

当一个或多个文件夹共享相同的显示名称时（例如，"Game Boy Advance (GBA)" 和 "Game Boy Advance (MGBA)"），它们将被合并为一个包含两个文件夹 ROM 的单一菜单项（继续前面的例子，"Game Boy Advance"）。这允许使用备用 pak 打开特定的 ROM。

----------------------------------------
BIOS

某些模拟器需要官方 BIOS 才能运行或表现更好。MinUI 严格遵守 BYOB（自带 BIOS）。将每个系统的 BIOS 放在与相应 "Roms" 文件夹名称中标签匹配的文件夹中（例如，"Sony PlayStation (PS)" ROM 的 BIOS 放在 "/Bios/PS/" 中）。

BIOS 文件名区分大小写：

   FC: disksys.rom
   GB: gb_bios.bin
  GBA: gba_bios.bin
  GBC: gbc_bios.bin
   MD: bios_CD_E.bin
       bios_CD_J.bin
       bios_CD_U.bin
   PS: psxonpsp660.bin

----------------------------------------
基于光盘的游戏

为了简化使用 MinUI 启动多文件光盘游戏，请将你的 bin/cue（和/或 iso/wav 文件）放在与 cue 文件同名的文件夹中。MinUI 在选择时将自动启动 cue 文件而不是导航到文件夹中，例如：

  Harmful Park (English v1.0)/
    Harmful Park (English v1.0).bin
    Harmful Park (English v1.0).cue

对于多碟游戏，将所有碟片的所有文件放在一个文件夹中。然后在该文件夹中创建一个 m3u 文件（只是一个文本文件，每行包含每个碟片 cue 文件的相对路径），文件名与文件夹名相同。MinUI 不会显示文件夹中杂乱的内容，而是启动相应的 cue 文件，例如，对于一个 "Policenauts" 文件夹结构如下：

  Policenauts (English v1.0)/
    Policenauts (English v1.0).m3u
    Policenauts (Japan) (Disc 1).bin
    Policenauts (Japan) (Disc 1).cue
    Policenauts (Japan) (Disc 2).bin
    Policenauts (Japan) (Disc 2).cue

m3u 文件将只包含：

  Policenauts (Japan) (Disc 1).cue
  Policenauts (Japan) (Disc 2).cue

当检测到多碟游戏时，游戏内菜单的 "继续" 项目还会显示当前碟片。按左右键在碟片之间切换。

MinUI 还支持 chd 文件和官方 pbp 文件（不支持大于 2GB 的多碟 pbp 文件）。无论使用哪种多碟文件格式，同一游戏的每个碟片共享相同的记忆卡和存档状态槽位。

----------------------------------------
合集合集

合集只是一个文本文件，包含按顺序排列的 ROM、cue 或 m3u 文件的完整路径。这些文本文件位于 SD 卡根目录的 "Collections" 文件夹中，例如，"/Collections/Metroid series.txt" 可能如下所示：

  /Roms/GBA/Metroid Zero Mission.gba
  /Roms/GB/Metroid II.gb
  /Roms/SNES (SFC)/Super Metroid.sfc
  /Roms/GBA/Metroid Fusion.gba

----------------------------------------

显示名称

某些（不支持的街机）核心要求 ROM 使用晦涩的文件名。你可以通过在要重命名的文件所在的同一文件夹中创建 map.txt 来覆盖整个 MinUI 中使用的显示名称。每个文件一行，`rom.ext` 后跟一个制表符，再后跟 `显示名称`。你可以通过在显示名称开头添加 `.` 来隐藏文件。例如：
	
  neogeo.zip	.Neo Geo Bios
  mslug.zip	Metal Slug
  sf2.zip	Street Fighter II

----------------------------------------
简单模式

对你来说还不够简单（或者也许是你的孩子）？MinUI 有一个简单模式，隐藏 Tools 文件夹并将游戏内菜单中的 "选项" 替换为 "重置"。非常适合交给小孩子（我想大人也可以）。只需在 "/.userdata/shared/" 中创建一个名为 "enable-simple-mode"（无扩展名）的空文件。

----------------------------------------
高级

MinUI 可以在启动时自动运行用户编写的 shell 脚本。只需将一个名为 "auto.sh" 的文件放在 "/.userdata/<DEVICE>/" 中。如果你使用 Windows，请确保你的文本编辑器使用 Unix 行尾（如 `\n`），这些设备通常无法处理 Windows 行尾（如 `\r\n`）。

----------------------------------------
致谢

感谢 eggs，感谢他的 NEON 缩放器、多年来的顶级示例代码，以及在我无休止的问题面前表现出的耐心。

查看 eggs 的发布（包含源代码）： 

  RG35XX https://www.dropbox.com/sh/3av70t99ffdgzk1/AAAKPQ4y0kBtTsO3e_Xlrhqha
  Miyoo Mini https://www.dropbox.com/sh/hqcsr1h1d7f8nr3/AABtSOygIX_e4mio3rkLetWTa
  Trimui Model S https://www.dropbox.com/sh/5e9xwvp672vt8cr/AAAkfmYQeqdAalPiTramOz9Ma

感谢 neonloop，感谢他将最初的 Trimui 工具链整合在一起，我从中学到了关于 docker 和 buildroot 的一切，这也是我后来整合的每个工具链的基础，以及 picoarch，minarch 的灵感来源。

查看 neonloop 的仓库： 

  https://git.crowdedwood.com

感谢 adixial、acmeplus 和整个 muOS 社区，感谢他们分享关于 Anbernic h700 系列设备的发现。

查看 muOS 和 Knulli：

	https://muos.dev
	https://knulli.org

感谢 fewt 和整个 JELOS 社区，感谢 JELOS（没有它 MinUI 就无法在 RGB30 上运行），以及与我这个永远的 Linux 内核新手分享他们的知识。

查看 JELOS：

  https://github.com/JustEnoughLinuxOS/distribution

感谢 Steward，感谢他为众多设备维护详尽的文档：

	https://steward-fu.github.io/website/

感谢 Gamma，感谢他在 MagicX XU Mini M 上解锁更多性能的努力（在我们所有人都意识到它的 RG3562 悄悄地是 RK3266 之前）。

查看他的仓库（包括 GammaOS）：

	https://github.com/TheGammaSqueeze/

感谢 BlackSeraph，感谢他向我介绍了 chroot。

查看 GarlicOS 仓库：

	https://github.com/GarlicOS

感谢 Jim Gray，感谢在开发过程中的共鸣、早期 alpha 测试，以及为 MinUI 的大部分开发提供配乐。

查看 Jim 的音乐： 

  https://ourghosts.bandcamp.com/music
  https://www.patreon.com/ourghosts/
 
