# Upstreaming status

This draft pull request is the public review entry for the D13x Hengshan Pi
port developed in `contest2026_011_ladelamuStudio`.

Current source baseline:

- contest pull request: `open-vela/contest2026_011_ladelamuStudio#11`;
- source commit: `d43191e91cd92b45ced82d17b71db0f9dc767f05`;
- firmware version: `1.11.15.8`.

This revision contains the latest Vendor-layer files changed by the contest
candidate:

- Hengshan Pi NSH `defconfig`;
- GT911 board integration using a low-priority polling worker;
- D133EBS Kconfig selections;
- LVDS framebuffer cache maintenance and frame-queue completion;
- SPI NOR partition layout and OS image description.

The pull request remains a draft because the remaining D13x boot, IRQ, UART,
I2C, display-controller, GMAC and board initialization files still need to be
split out of the contest repository and reviewed as focused follow-up commits.
The files currently included are not claimed to form a standalone build yet.

Generic changes under `open-vela/nuttx`, including RISC-V FPU and common input
driver work, are intentionally excluded and will be submitted separately.
