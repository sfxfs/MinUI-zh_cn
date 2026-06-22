# MinUI

MinUI 是一个专注的自定义启动器和 libretro 前端，支持[多种复古掌机](#支持设备)。

<img src="github/minui-main.png" width=320 /> <img src="github/minui-menu-gbc.png" width=320 /> 

## 功能特点

- 简洁的启动器，简洁的 SD 卡
- 无需设置或配置
- 无封面、主题或干扰元素
- 自动隐藏隐藏文件
  以及显示名称中的扩展名和区域/版本信息
- 统一的模拟器内菜单，
  可快速访问存档状态、换碟
  和模拟器选项
- 30 秒后自动休眠，
  或按 POWER 键休眠（和唤醒）
- 休眠后两分钟自动关机，
  或长按 POWER 键一秒关机
- 如果在游戏中关机（手动或休眠），
  自动恢复到离开时的状态
- 在启动器中按 X 而非 A 
  可从手动创建的最近存档状态恢复
- 精简的模拟器前端
  （minarch + libretro 核心）
- 单张 SD 卡兼容来自不同
  制造商的多款设备

你可以[在这里获取最新版本](https://github.com/shauninman/MinUI/releases)。

> 带有物理电源开关的设备
> 使用 MENU 键代替 POWER 键
> 进行休眠和唤醒。休眠后可以
> 安全地使用开关手动关机。

## 支持的主机

基础：

- Game Boy
- Game Boy Color
- Game Boy Advance
- Nintendo Entertainment System
- Super Nintendo Entertainment System
- Sega Genesis
- PlayStation

扩展：

- Neo Geo Pocket（及 Color）
- Pico-8
- Pokémon mini
- Sega Game Gear
- Sega Master System
- Super Game Boy
- TurboGrafx-16（及 TurboGrafx-CD）
- Virtual Boy

## 支持设备

| 设备 | 添加版本 | 状态 |
| -- | -- | -- |
| Anbernic RG28xx | MinUI-20240429b-2 | 旧版 |
| Anbernic RG34xx | MinUI-20241227-0 | 旧版 |
| Anbernic RG34xxSP | MinUI-20250920-0 | 旧版 |
| Anbernic RG35xx | MinUI-20230922b-2 | 旧版 |
| Anbernic RG35xx Plus | MinUI-20240106b-0 | 旧版 |
| Anbernic RG35xxH | MinUI-20240120b-1 | 旧版 |
| Anbernic RG35xxSP | MinUI-20240525-0 | 旧版 |
| Anbernic RG40xxH | MinUI-20240717-1 | 旧版 |
| Anbernic RG40xxV | MinUI-20240831-0 | 旧版 | 
| Anbernic RG CubeXX | MinUI-202401028-0 | 旧版 | 
| GKD Pixel | MinUI-20240120b-1 | 旧版 |
| M17 | MinUI-20231126b-2 | 旧版 |
| MagicX XU Mini M | MinUI-20240831-0 | 旧版 | 
| MagicX Mini Zero 28 | MinUI-20250111-0 | 旧版 |
| Miyoo A30 | MinUI-20240705-0 | 旧版 |
| Miyoo Flip | MinUI-20250111-0 | 旧版 |
| Miyoo Mini | MinUI-20230922b-2 | 旧版 |
| Miyoo Mini Flip | MinUI-20251023-0 | 旧版 |
| Miyoo Mini Plus | MinUI-20230922b-2 | 旧版 |
| Powkiddy RGB30 | MinUI-20231014b-1 | 旧版 |
| Trimui Brick | MinUI-20241028-0 | 旧版 |
| Trimui Smart | MinUI-20230922b-2 | 旧版 |
| Trimui Smart Pro | MinUI-20231111b-2 | 旧版 |

> [!NOTE]
> **活跃** — 正在积极为此设备进行兼容性和改进工作  
> **维护** — 继承通用功能的改进  
> **旧版** — 将在未来更新中停用  
> **已停用** — 已从仓库中移除，不再更新或打包到新版本中

## 旧版存档

最初的 Trimui Model S 版本的 MinUI（2021/04/03-2021/08/06）已存档于[此处](https://github.com/shauninman/MinUI-Legacy-Trimui-Model-S)。

后续的 MiniUI for Miyoo Mini（2022/04/20-2022/10/23）已存档于[此处](https://github.com/shauninman/MiniUI-Legacy-Miyoo-Mini)。

MinUI 回归最初的 Anbernic RG35XX（2023/02/26-2023/03/26）已存档于[此处](https://github.com/shauninman/MinUI-Legacy-RG35XX)。

当前版本的 MinUI 从 Trimui Smart、Miyoo Mini（及 Plus）和最初的 Anbernic RG35XX 开始引入了多设备支持，发布于 [2023/09/22][init-release]，初始功能提交则在 6 个月前的 [2023/03/27][init-commit]。

[init-release]:https://github.com/shauninman/MinUI/releases/tag/v20230922b-2
[init-commit]:https://github.com/shauninman/MinUI/commit/53e0296ea5a2794290fb5783765af6cee0063445#diff-b993e61ab6e66a19b67c88cfb98261aa9267d250de8bb56463662f67aae1a558
