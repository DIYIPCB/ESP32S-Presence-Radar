# ESP32S Presence Radar

**[Buy the kit on ESP32S — USD $29](https://esp32s.com/product/esp32s-presence-radar/)** · [Product Wiki](https://esp32s.com/wiki/esp32s-presence-radar/)

Kit: assembled ESP32-S3 mainboard + HLK-LD2410C radar + connection cable. No enclosure, USB cable or power adapter. Made to order: 5-day production lead time after order/payment confirmation; dispatch after production and checks. Shipping transit time is additional.

R1 engineering prototype. Hardware has not yet been powered on or qualified. Complete Wi-Fi CSI firmware is not included.

![Mainboard 3D front](presence-radar-3d-front.png)
![Mainboard 3D back](presence-radar-3d-back.png)

Mainboard images are KiCad 3D renders, not delivered-product photographs. The external radar and connection cable are not shown.

## Complete open design

**[Download the complete editable design archive](ESP32S-Presence-Radar-open-source.zip)** ([direct download](https://github.com/DIYIPCB/ESP32S-Presence-Radar/raw/refs/heads/main/ESP32S-Presence-Radar-open-source.zip)).

Unpack the archive and open `ESP32S-Presence-Radar/presence_radar_csi_r1.kicad_pro` in KiCad 10. The archive preserves all project-relative paths and includes:

- KiCad schematic, PCB and project; local symbols and pinned footprints.
- Mainboard BOM, connectivity, prototype Gerbers, drill and placement files.
- Board previews, engineering notes and manufacturer datasheet links.
- Radar-only ESPHome configuration (uncompiled), local secrets template, Python fusion reference and six tests.
- Complete licence texts and third-party attribution notices.

The archive is the canonical source distribution; use its complete directory when editing the board. KiCad 10 standard 3D models must be installed.

## Hardware and interfaces

45 × 50 mm, two-layer, 1.6 mm FR-4 board. ESP32-S3-WROOM-1-N8R8 with built-in antenna, USB-C 5 V power/data, 3.3 V buck supply, RESET/BOOT buttons and status LED. No battery or charging circuit. Antenna and USB may extend beyond the board envelope.

| Interface | Pins |
| --- | --- |
| J1 USB-C | VBUS 5 V; D− GPIO19; D+ GPIO20; GND; CC1/CC2 pulldowns |
| J2 radar | 1 TX → GPIO5; 2 RX ← GPIO4; 3 OUT → GPIO6; 4 GND; 5 VCC 5 V |
| J3 I²C | 1 3V3; 2 GND; 3 GPIO8 SDA; 4 GPIO9 SCL |
| J4 debug | 1 GND; 2 GPIO43 TX0; 3 GPIO44 RX0; 4 GPIO10 |

J2 TX/RX names follow the radar; J4 TX0/RX0 follow the ESP32. Radar UART: 256000 baud, 3.3 V logic. SW1 RESET controls EN; SW2 BOOT controls GPIO0.

## Software and checks

Radar is the primary sensing source. Wi-Fi CSI remains a development route requiring suitable Wi-Fi traffic, firmware integration and environmental calibration. See [Espressif ESP-CSI](https://github.com/espressif/esp-csi).

`fusion_reference.py` is a Python specification, not ESP32 firmware or a CSI detector. It permits one bounded 5-second CSI departure grace; radar failure reports unknown. Six rule tests pass.

Saved checks dated 2026-10-14: ERC 0, DRC 0, no unconnected items and schematic/PCB parity 0. Ideal reset RC simulation: approximately 10.08 ms. Hardware power, USB, EMC/ESD, thermal, RF and presence accuracy remain unverified; the design is not production-qualified.

## Licence

Original hardware/manufacturing data: [CERN-OHL-P-2.0](CERN-OHL-P-2.0.txt). Original code, documentation and renders: [MIT](MIT.txt). Redistributed KiCad libraries retain [CC-BY-SA-4.0](CC-BY-SA-4.0.txt) with the [KiCad library exception](KICAD-LICENSE.md). Full scope and notices are included in the source archive.

Product brand: ESP32S · www.esp32s.com · PCB manufactured by DIYIPCB. Brand markings are not evidence of physical manufacturing. No trademark rights or third-party endorsement are granted.
