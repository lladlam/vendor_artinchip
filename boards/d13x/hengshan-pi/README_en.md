# openvela Support for the D13x Hengshan Pi Board

[ [简体中文](README.md) | English ]

## Introduction

This directory is the upstreaming entry for **ArtInChip D13x / D133EBS
Hengshan Pi** board support in openvela. The port originates from the 2026
openvela AI Hardware Developer Contest project
[`contest2026_011_ladelamuStudio`](https://github.com/open-vela/contest2026_011_ladelamuStudio).

The contest implementation has been verified on hardware from PBP/tinySPL
through NuttX and NSH to an LVGL connected-home panel. This pull request is
being upstreamed in stages: first agree on the directory layout and porting
boundaries, then add the board, chip and packaging code in reviewable commits.

> **Branch dependency**
>
> The current port is based on `dev-ai-contest-2026` and depends on the same
> branch of `open-vela/nuttx`. Generic RISC-V, FPU and input-driver fixes will
> be proposed separately to `open-vela/nuttx` rather than mixed into this
> vendor pull request.

## Verified capabilities

| Capability | Status | Notes |
| --- | --- | --- |
| Boot chain | Verified | PBP/tinySPL loads NuttX and enters NSH |
| UART0 | Verified | 115200 8N1 console |
| LVDS display | Verified | 1024×600 RGB565, `/dev/fb0` |
| GT911 touch | Verified | Capacitive touch, `/dev/input0` |
| I2C | Verified | Used by the touch controller |
| System timer | Verified | CORET/GTC drives the system tick |
| GMAC0 Ethernet | Verified | RMII 100M, DHCP, DNS and ICMP |
| SPI NOR | Verified | 16 MiB layout for system, font and persistent data |
| LVGL application | Verified | Home, room and device synchronization/control demo |

## Planned upstream layout

```text
vendor/artinchip/
├── boards/d13x/hengshan-pi/   # board init, configs, linker and pack inputs
└── chips/d13x/                # D13x boot, IRQ, UART, I2C, display and network
```

The planned commit series is:

1. Board documentation and directory convention;
2. D13x boot, memory, interrupt and UART foundation;
3. Hengshan Pi board initialization and `defconfig`;
4. LVDS, I2C, GT911, system timer and GMAC0;
5. SPI NOR partitioning and image packaging;
6. Build, hardware validation and XTS/stability records.

## Current implementation

The runnable contest version remains available in the dedicated repositories:

- [Official contest repository](https://github.com/open-vela/contest2026_011_ladelamuStudio)
- [Developer fork](https://github.com/lladlam/contest2026_011_ladelamuStudio)

Until the upstream cleanup is complete, the contest repository keeps the
required overlays and integration scripts so the submitted project remains
reproducible.

## License

New original source files in this directory are intended to use Apache-2.0 and
will retain SPDX identifiers or the standard Apache license header. Boot
binaries, fonts and third-party components will document their source and
license boundaries separately.
