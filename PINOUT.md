# NM-CYD-C5 GPIO Pinout — GhostESP Firmware

You can wire modules directly to these GPIO pins without the NM-BR-bot HAT.
The firmware uses these pins regardless of whether the HAT is attached.

---

## Shared SPI Bus (SPI2)
Display, SD card, and NRF24 all share the same SPI2 bus.
Only one CS/CSN line is pulled low at a time.

| Signal    | GPIO |
|-----------|------|
| MOSI      | IO7  |
| MISO      | IO2  |
| CLK/SCK   | IO6  |

---

## Display — ST7789 2.8" 240x320

| Signal | GPIO |
|--------|------|
| CS     | IO23 |
| DC     | IO24 |
| BL     | IO25 |
| RST    | —    |

---

## Touchscreen — XPT2046 (shares SPI2)

| Signal | GPIO |
|--------|------|
| CS     | IO1  |

---

## SD Card (shares SPI2)

| Signal | GPIO |
|--------|------|
| CS     | IO10 |

---

## NFC — PN532 (I2C)

| Signal | GPIO |
|--------|------|
| SCL    | IO8  |
| SDA    | IO9  |
| IRQ    | —    |
| RST    | —    |

---

## IR (shares GPIO with NFC via DIP switch on HAT)

| Signal | GPIO |
|--------|------|
| TX/LED | IO8  |
| RX     | IO9  |

> **Note:** IR and NFC share IO8/IO9. Do not use both at the same time.
> On the HAT this is handled by DIP switches. If wiring directly, only
> connect one module to these pins at a time.

---

## NRF24L01 (shares SPI2)

| Signal | GPIO |
|--------|------|
| MOSI   | IO7  |
| MISO   | IO2  |
| SCK    | IO6  |
| CSN    | IO10 |
| CE     | IO5  |

> **Note:** NRF24 CSN shares IO10 with SD card CS. Do not use both
> simultaneously without the HAT's DIP switch isolation.

---

## GPS (UART RX only)

| Signal   | GPIO | Baud  |
|----------|------|-------|
| RX       | IO5  | 9600  |

> Connect GPS TX → IO5. Only RX is used (read-only).

---

## UART (USB-UART header)

| Signal | GPIO |
|--------|------|
| TX     | IO11 |
| RX     | IO12 |
