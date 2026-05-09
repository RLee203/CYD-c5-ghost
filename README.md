# GhostESP — NM-CYD-C5 Firmware (IR + BLE + Portal Fixes)

Pre-built firmware for the **NM-CYD-C5** board (ESP32-C5 + 2.8" ST7789 touchscreen).

## Hardware

- **Board:** NM-CYD-C5
- **MCU:** ESP32-C5
- **Display:** 2.8" ST7789 320x240 touchscreen
- **HAT:** NM-BR-bot (CC1101, NRF24, PN532 NFC, IR TX/RX, 433MHz via DIP switches)

## What's Fixed in This Build

- **IR Dazzler** — was not emitting. GPIO 8 was left in open-drain mode after NFC I2C teardown, blocking RMT output. Fixed.
- **BLE Wardriving** — scans were failing silently after WiFi mode switch. Added settle delay so BLE initializes cleanly.
- **Captive Portal** — portal webserver failed to start due to socket limit. Raised LWIP socket pool and corrected max_open_sockets.
- **HTTP server** — EADDRINUSE on restart after BLE session. Fixed with escalating retry delays.

## Working Features

- WiFi wardriving, deauth, beacon spam, evil portal
- BLE wardriving
- NFC (PN532) — scan and save to SD card
- IR dazzler and IR transmit
- NRF24
- SD card saves (long filenames supported)

## Flashing

Requires [esptool](https://github.com/espressif/esptool) (`pip install esptool`).

```bash
python -m esptool --chip esp32c5 --port COM4 --baud 460800 \
  write_flash --flash_mode dio --flash_size 16MB --flash_freq 80m \
  0x2000  bootloader.bin \
  0x8000  partition-table.bin \
  0x10000 Ghost_ESP_IDF.bin
```

## Notes

- **BLE Detect Devices** only shows Flipper Zero, AirTags, and suspected skimmers — not all BLE devices. This is by design.
- NM-BR-bot HAT modules share GPIO 8/9 via DIP switches. Only one module active at a time (NFC or IR, not both).
