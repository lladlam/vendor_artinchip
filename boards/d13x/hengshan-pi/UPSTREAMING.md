# Upstreaming status

This draft pull request is the public review entry for the D13x Hengshan Pi
port developed in `contest2026_011_ladelamuStudio`.

The first revision intentionally contains documentation only. Board, chip and
packaging changes will be added as focused follow-up commits after maintainers
confirm the target directory layout. Keeping the initial diff non-invasive
avoids modifying existing build paths before the layout is agreed.

Tracked code groups:

- board initialization and `defconfig`;
- D13x boot, IRQ, UART and memory support;
- LVDS framebuffer and GT911 touch;
- CORET/GTC system timer;
- GMAC0 RMII Ethernet;
- SPI NOR partitions and image packaging.

Generic changes under `open-vela/nuttx` are intentionally excluded and will be
submitted through separate pull requests.
