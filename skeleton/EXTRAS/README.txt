MinUI 是一个极简启动器，支持 RGB30、Trimui Smart（及 Pro）、Miyoo Mini（及 Plus）、M17 和 RG35XX——全部来自同一张 SD 卡。为什么？何乐而不为呢？

源码：
https://github.com/shauninman/minui

----------------------------------------
安装

前言

在支持双 SD 卡的设备上（如 RG35XX），我将使用 "TF1" 来指代插入设备第一个插槽的卡。所有其他提到的 "SD 卡" 或 "主卡" 指的是插入第二个插槽的卡，或仅支持单卡设备的唯一 SD 卡。为了在支持双 SD 卡的设备上获得最佳体验，你应该将 MinUI 安装在第二张卡上。

将此 zip 文件中的所有文件夹复制到主卡的根目录。

----------------------------------------
更新

此扩展 zip 文件随每个版本发布，无论其内容是否更改。请参阅发布说明以查看添加或更改了哪些内容，并将所需的更新 pak 复制到 Emus 或 Tools 文件夹中的相应设备文件夹中（例如 /Emus/tg5040 或 /Tools/rgb30）。

----------------------------------------
BIOS 文件

你需要为此 zip 文件中包含的模拟器 pak 自带 BIOS。

MGBA: gba_bios.bin
 PCE: syscard3.pce
 PKM: bios.min
 SGB: sgb.bios

----------------------------------------
原生 PICO-8 和 Splore.pak（仅限 RGB30）

从 https://lexaloffle.itch.io/pico-8 下载适用于 Raspberry Pi 的官方 PICO-8 幻想主机（如果你在过去几年中在 itch.io 上购买过捆绑包，你可能已经在库中有了副本 https://itch.io/my-collections）。在撰写本文时，文件名为 "pico-8_0.2.5g_raspi.zip"。将该 zip 文件复制到 "/Tools/rgb30/Splore.pak/" 中。将 "/Emus/rgb30/P8-NATIVE.pak"、"/Tools/rgb30/Splore.pak" 和 "/Tools/rgb30/Wi-Fi.pak" 复制到你的 SD 卡。（你需要 Wi-Fi.pak 来在 Splore.pak 中下载 PICO-8 游戏。）

将你想用原生 PICO-8 玩的卡带放在 "/Roms/Pico-8 (P8-NATIVE)/" 中。

要退出 P8-NATIVE.pak，按 start。然后选择 "SHUTDOWN"。

要退出 Splore.pak，按 start。在游戏中选择 "EXIT TO SPLORE"。在 splore 中选中一个卡带后按 start，选择 "OPTIONS"，然后选择 "SHUTDOWN PICO-8"。

请注意，Splore.pak 和 P8-NATIVE.pak 没有/无法实现 MinUI 的统一功能，如游戏内菜单（包括存档状态）、模拟休眠和快速存档/自动恢复。

----------------------------------------
Wi-Fi.pak（仅限 RGB30）

在纯文本编辑器中打开 "wifi.txt"，在两行中分别输入你的网络名称和密码并保存，例如：

  minui
  lessismore

将 "Wi-Fi.pak" 复制到 SD 卡上的 "/Tools/rgb30/"。第一次打开 pak（或每次更改 "wifi.txt" 内容时）将更新网络名称和密码然后连接。后续启动将切换 Wi-Fi 开关。Wi-Fi 会消耗电池，因此最好仅在计划使用时启用，使用完毕后禁用。你的 Wi-Fi 状态在重启后保持。

----------------------------------------
Remove Loading.pak（Miyoo A30）

此 pak 移除开机时出现在启动徽标和主界面之间的 "LOADING" 文本。它需要修补 NAND 内存以修改原本只读的根文件系统。完成大约需要 5 分钟。虽然不是必需的，但在执行此操作时连接电源是非常好的主意。请耐心等待，在完成之前不要关闭设备。

----------------------------------------
Remove Loading.pak（Trimui Smart Pro 和 Brick）

此 pak 移除开机时出现在启动徽标和主界面之间的 "LOADING" 文本。与 A-30 相比，这是一个微创操作。不用担心。

----------------------------------------
Swap Menu.pak（RG34XX）

此 pak 在系统级别交换 MENU 和 SELECT 按钮，使 MENU 更容易访问。启动 pak 然后重启。重新启动 pak 并重启以撤销更改。
