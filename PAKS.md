# 关于 MinUI Pak

Pak 只是一个带有 ".pak" 扩展名的文件夹，其中包含一个名为 "launch.sh" 的 shell 脚本。

有两种类型的 pak：模拟器和工具。模拟器 pak 位于 Emus 文件夹中。工具 pak 位于 Tools 文件夹中。这两个文件夹位于 SD 卡的根目录。额外的 pak 不应添加到 SD 卡根目录的隐藏 ".system" 文件夹中。每次用户更新 MinUI 时，此文件夹都会被删除和替换。

Pak 是特定于平台的。在 Emus 和 Tools 文件夹中，你会找到（或需要创建）平台文件夹。一些平台文件夹以目标设备命名（例如，Powkiddy RGB30 的 "rgb30"），其他使用设备的内部名称（例如，Trimui Smart Pro 的 "tg5040"），其他使用任意简称（例如，Trimui Model S 的 "trimui"），全部为小写。请参阅扩展包以获取最新的支持平台文件夹名称。

某些平台有多个具有独特特性的设备。MinUI 使用 `DEVICE` 环境变量来区分这些设备与基础平台。例如，"rg35xxplus" 平台有两个独特设备：RG CubeXX 的 "cube" 和 RG34xx 的 "wide"。它还支持输出到 HDMI 时的 "hdmi"。Pak 可以选择使用或忽略此环境变量。

# 模拟器 Pak 的类型

有三种基本类型的模拟器 pak，选择哪种取决于你的目标和你期望的 MinUI 集成程度。

第一种类型重用基础 MinUI 安装中包含的 libretro 核心。这利用了已知可工作的核心，但允许自定义默认选项和分离用户配置。此类型的一个例子是额外的 GG.pak，它使用默认的 picodrive 核心。

第二种类型包含自己的 libretro 核心。这允许你支持全新的系统，同时仍然利用 MinUI 的标准功能，如从菜单恢复、快速存档和自动恢复，以及一致的游戏内菜单、行为和选项。此类型的一个例子是额外的 MGBA.pak，它捆绑了自己的 mgba 核心。

第三种类型启动捆绑的独立模拟器。这可能允许你从硬件中挤出比 libretro 核心更多的性能。此类型的缺点是与 MinUI 没有集成。没有从菜单恢复，没有快速存档和自动恢复，没有一致的游戏内菜单、行为或选项。在某些情况下，MENU（如果有 POWER）按钮可能无法按预期工作，甚至完全不工作。此类型的 pak 应该是最后的手段。此类型的一个例子是社区开发的 NDS.pak，它适用于 MinUI 支持的少数平台。

在所有情况下，请向你的用户明确说明我（@shauninman）无法支持第三方 pak。如果我将某个主机或核心排除在 MinUI 的基础或扩展包之外，通常有充分的理由，要么是核心的集成不够完善（例如，街机核心期望 ROM 具有特定的、晦涩的文件名，只有某些 ROM 集适用于某些核心），有太多错误（例如，无法可靠地从存档状态恢复），在特定设备上性能不佳，或者只是我不熟悉或不感兴趣的主机。

# 命名你的模拟器 Pak

MinUI 根据 ROM 父文件夹名称末尾括号中的标签将 ROM 映射到 pak（例如，"/Roms/Game Boy (GB)/Dr. Mario (World).gb" 将启动 "GB.pak"）。标签应全部大写。选择标签时，从其他模拟器前端（如 Retroarch 或 EmulationStation）使用的常见缩写开始（例如，Famicom/Nintendo 的 FC 或 MegaDrive/Genesis 的 MD）。如果该标签已被另一个 pak 使用，请使用核心名称（如果较短，例如 MGBA）或核心名称的缩写（例如，pokemini 的 PKM）或截断（例如，mednafen_supafaust 的 SUPA）。

# 启动你的核心

这是一个示例 "launch.sh"：

	#!/bin/sh
	
	EMU_EXE=picodrive
	
	###############################
	
	EMU_TAG=$(basename "$(dirname "$0")" .pak)
	ROM="$1"
	mkdir -p "$BIOS_PATH/$EMU_TAG"
	mkdir -p "$SAVES_PATH/$EMU_TAG"
	HOME="$USERDATA_PATH"
	cd "$HOME"
	minarch.elf "$CORES_PATH/${EMU_EXE}_libretro.so" "$ROM" &> "$LOGS_PATH/$EMU_TAG.txt"

这将使用基础 MinUI 安装中包含的 "picodrive\_libretro.so" 核心打开请求的 ROM。要使用不同的核心，只需将 `EMU_EXE` 的值更改为另一个核心名称（去掉 "_libretro.so"）。如果该核心捆绑在你的 pak 中，请在 `EMU_EXE` 行之后添加以下内容：

	CORES_PATH=$(dirname "$0")

不需要编辑分隔线以下的任何内容。其余部分是样板代码，将从文件夹名称中提取 pak 的标签，创建相应的 BIOS 和保存文件夹，将 `HOME` 环境变量设置为 "/.userdata/[platform]/"，启动游戏，并将 minarch 和核心的任何输出记录到 "/.userdata/[platform]/logs/[TAG].txt"。

就是这样！尽情尝试来自原厂固件、其他兼容设备的核心，或自己构建的核心吧。

哦，如果你正在为 Anbernic 的 RG*XX 系列创建 pak，你需要将最后一行的最后部分从 ` &> "$LOGS_PATH/$EMU_TAG.txt"` 改为 ` > "$LOGS_PATH/$EMU_TAG.txt" 2>&1`，因为它的默认 shell 有问题。

# 选项默认值和按钮绑定

将你的新 pak 和一些 ROM 复制到 SD 卡并启动游戏。按 MENU 按钮并选择 "选项"。配置 "前端"、"模拟器" 和 "控制"。MinUI 的标准做法是只绑定原始系统物理控制器上存在的按钮（例如，没有连发按钮或核心特定功能，如调色板或换碟）。让玩家自己去挖掘这些，"快捷键" 也是如此。最后选择 "保存更改" > "保存为本机设置"。然后退出并将 SD 卡插回计算机。

在 SD 卡根目录的隐藏 ".userdata" 文件夹中，你会找到平台文件夹，在你的平台文件夹中有一个 "[TAG]-[core]" 文件夹。将其中找到的 "minarch.cfg" 文件复制到你的 pak 文件夹并重命名为 "default.cfg"。打开 "default.cfg" 并删除你没有自定义的任何选项。任何以 "-" 为前缀的选项名称将被设置并隐藏。这对于禁用在特定平台上可能不可用（例如，超频）或性能不佳（例如，缩放）的功能很有用。在文件底部附近你会找到按钮绑定。以下是 "MGBA.pak" 的一个例子：

	bind Up = UP
	bind Down = DOWN
	bind Left = LEFT
	bind Right = RIGHT
	bind Select = SELECT
	bind Start = START
	bind A Button = A
	bind B Button = B
	bind A Turbo = NONE:X
	bind B Turbo = NONE:Y
	bind L Button = L1
	bind R Button = R1
	bind L Turbo = NONE:L2
	bind R Turbo = NONE:R2
	bind More Sun = NONE:L3
	bind Less Sun = NONE:R3

`bind ` 之后到 `=` 之前的所有内容是将出现在 "控制" 菜单中的按钮标签。我通常会规范化这些标签（例如，"Up" 而不是 "D-pad up"，"A Button" 而不是仅仅 "A"）。`=` 之后到可选的 `:` 之前的所有内容是按钮映射。按钮映射全部大写。肩键和模拟摇杆按钮始终包含数字（例如，"L1" 而不是仅仅 "L"）。如果按钮默认不应绑定，请使用 "NONE"。在自定义或移除绑定时，应始终在 ":" 后添加默认的核心定义按钮映射。在上面的例子中，我通过以下更改移除了默认的 "More Sun" 绑定：

	bind More Sun = L3

改为

	bind More Sun = NONE:L3

# 亮度和音量

某些二进制文件坚持在每次启动时重置亮度（例如，40xxH 原厂固件上的 DinguxCommander）或音量（例如，所有平台上的 ppssppSDL）。为了与 MinUI 的全局设置保持同步，有 syncsettings.elf。它等待一秒钟，然后恢复 MinUI 当前的亮度和音量设置。在大多数情况下，你可以在启动二进制文件之前将其作为守护进程启动：

	syncsettings.elf &
	./DinguxCommander

但如果二进制文件初始化需要超过一秒钟，你可能需要让它在二进制文件运行的整个时间内循环运行：

	while :; do
	    syncsettings.elf
	done &
	LOOP_PID=$!
	
	./PPSSPPSDL --pause-menu-exit "$ROM_PATH"
	
	kill $LOOP_PID

# 注意事项

MinUI 目前仅支持 RGB565 像素格式，不实现 OpenGL libretro API。可以使用原厂固件的 retroarch 代替 MinUI 的 minarch 来运行某些核心，但这留给读者作为练习。
