# D13x 衡山派开发板对 openvela 的支持

[ 简体中文 | [English](README_en.md) ]

## 简介

本目录用于向 openvela 上游提交 **ArtInChip D13x / D133EBS 衡山派**开发板支持。
该适配来源于 2026 首届 openvela AI 硬件开发者大赛项目
[`contest2026_011_ladelamuStudio`](https://github.com/open-vela/contest2026_011_ladelamuStudio)。

当前比赛仓已经在开发板实机上完成从 PBP/tinySPL 到 NuttX、NSH 和 LVGL
家庭中控应用的完整启动与运行验证。本 PR 采用分阶段方式上游：先确认目录布局和
适配边界，再逐步加入板级、芯片级和打包代码。

> **分支依赖**
>
> 适配当前以 `dev-ai-contest-2026` 为基线，并依赖同分支的
> `open-vela/nuttx`。部分通用 RISC-V、FPU 和输入驱动修复将单独提交到
> `open-vela/nuttx`，不会混入 Vendor PR。

## 已验证能力

| 能力 | 当前状态 | 说明 |
| --- | --- | --- |
| 启动链路 | 已验证 | PBP/tinySPL 加载 NuttX 并进入 NSH |
| UART0 | 已验证 | 115200 8N1 控制台 |
| LVDS 显示 | 已验证 | 1024×600 RGB565，设备节点 `/dev/fb0` |
| GT911 触摸 | 已验证 | 电容触摸，设备节点 `/dev/input0` |
| I2C | 已验证 | 用于触摸控制器通信 |
| 系统定时器 | 已验证 | CORET/GTC 驱动系统 Tick |
| GMAC0 以太网 | 已验证 | RMII 100M、DHCP、DNS、ICMP |
| SPI NOR | 已验证 | 16 MiB 分区、系统镜像、字体和持久化数据 |
| LVGL 应用 | 已验证 | 家庭、房间、设备同步和控制 Demo |

## 计划上游内容

```text
vendor/artinchip/
├── boards/d13x/hengshan-pi/   # 板级初始化、配置、链接脚本和打包输入
└── chips/d13x/                # D13x 启动、中断、UART、I2C、显示和网络支持
```

计划拆分为以下提交：

1. 开发板文档与目录约定；
2. D13x 芯片启动、内存、中断和串口基础支持；
3. 衡山派板级初始化与 `defconfig`；
4. LVDS、I2C、GT911、系统定时器和 GMAC0；
5. SPI NOR 分区与镜像打包；
6. 构建、实机验证和 XTS/稳定性记录。

## 当前代码

比赛期间可运行版本暂时保存在专属比赛仓：

- [官方比赛仓](https://github.com/open-vela/contest2026_011_ladelamuStudio)
- [开发者 Fork](https://github.com/lladlam/contest2026_011_ladelamuStudio)

在本 PR 完成上游整理前，比赛仓仍保留必要的 Overlay 和集成脚本，以保证作品可复现。

## 许可证

本目录新增原创代码计划采用 Apache-2.0 许可证，并在源文件中保留 SPDX 或标准
Apache 许可证头。引入的启动二进制、字体和第三方组件将分别说明来源和许可边界。
