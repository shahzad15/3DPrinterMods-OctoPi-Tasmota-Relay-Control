# 🔌 OctoPi + Tasmota Smart Plug & Relay Automation Guide

Official open-source repository for **Automated Power Control, Remote Shutdown & Emergency Thermal Cutoff** for 3D printers using OctoPi (Raspberry Pi running OctoPrint) connected to Sonoff / ESP8266 Tasmota Smart Plugs or optocoupler 5V relay modules.

[![Photorealistic Vero Board Hardware Prototype](https://3dprintermods.xyz/wp-content/uploads/2026/08/tasmota_veroboard_real.jpg)](https://3dprintermods.xyz/2026/08/28/octopi-tasmota-smart-relay-power-control-guide/)

## 🌐 Full Step-by-Step Article & Setup Documentation
* 📖 **Complete Article Guide**: [https://3dprintermods.xyz/2026/08/28/octopi-tasmota-smart-relay-power-control-guide/](https://3dprintermods.xyz/2026/08/28/octopi-tasmota-smart-relay-power-control-guide/)
* 🔌 **5-Wire SWD RPi Bitbang Guide**: [https://3dprintermods.xyz/2026/08/28/5-wire-swd-rpi-bitbang-flashing-guide-unbrick-bigtreetech-skr-mainboards/](https://3dprintermods.xyz/2026/08/28/5-wire-swd-rpi-bitbang-flashing-guide-unbrick-bigtreetech-skr-mainboards/)
* 📡 **Wireless SWD ESP32 Guide**: [https://3dprintermods.xyz/2026/08/28/wireless-swd-firmware-updates-unbricking-over-wi-fi-esp32-bridge-guide/](https://3dprintermods.xyz/2026/08/28/wireless-swd-firmware-updates-unbricking-over-wi-fi-esp32-bridge-guide/)
* 🏠 **3D Printer Mods Lab**: [https://3dprintermods.xyz](https://3dprintermods.xyz)

---

## 📌 1. Hardware Pinout & Optocoupler Circuit Wiring

| Component Signal | ESP8266 / Sonoff Pin | Optocoupler PC817 Pin | Raspberry Pi GPIO Pin |
| :--- | :--- | :--- | :--- |
| **Relay Control** | GPIO 12 / D6 | Pin 1 (Anode) | GPIO 17 (Pin 11) |
| **Opto Cathode** | GND | Pin 2 (Cathode) | Ground (Pin 9) |
| **Relay Drive Signal** | 5V VCC | Pin 3 (Collector) | NPN Base (Q1) |
| **Relay Coil Ground** | GND | Pin 4 (Emitter) | GND |

> 💡 **Optocoupler Isolation Note:** The PC817 optocoupler completely isolates your Raspberry Pi 3.3V logic circuit from the 5V relay coil and high-voltage AC mains.

---

## ⚡ 2. Tasmota HTTP REST API Commands

```bash
# Toggle Relay Power ON
curl -s "http://192.168.1.150/cm?cmnd=Power%20ON"

# Toggle Relay Power OFF
curl -s "http://192.168.1.150/cm?cmnd=Power%20OFF"

# Query Power State Status
curl -s "http://192.168.1.150/cm?cmnd=Power"
```

---

## 📄 3. OctoPrint Tasmota Plugin Payload (`octoprint_tasmota_config.json`)

```json
{
  "ip_address": "192.168.1.150",
  "idx": "1",
  "auto_connect": true,
  "auto_connect_delay": 5,
  "auto_disconnect": true,
  "auto_off": true,
  "auto_off_delay": 10,
  "thermal_runaway_cutoff": true,
  "max_temp_limit": 305
}
```

---

## 🛒 Recommended Hardware Deals

| Hardware Component | Product Deal |
| :--- | :--- |
| **Raspberry Pi 4 Model B (Quad-Core BCM2711, 2.4/5GHz Wi-Fi)** | <a href="https://s.click.aliexpress.com/e/_c3kzgW2F" target="_blank"><img src="https://ae01.alicdn.com/kf/S3c738398848d44eeb3d2f1b8a01c6ab8x.png_80x80.png" width="80" height="80" /></a><br>[**Shop Raspberry Pi 4 Deal →**](https://s.click.aliexpress.com/e/_c3kzgW2F) |
| **WEMOS D1 Mini V4.0.0 Type-C USB WiFi Board (ESP8266 4MB)** | <a href="https://s.click.aliexpress.com/e/_c41U1LKR" target="_blank"><img src="https://ae01.alicdn.com/kf/S575dd42364e6406d8ce64f97b162ef0bM.jpg_80x80.jpg" width="80" height="80" /></a><br>[**Shop WEMOS D1 Mini Deal →**](https://s.click.aliexpress.com/e/_c41U1LKR) |
| **BigTreeTech SKR 3 & SKR Mini E3 V3.0 Mainboard** | <a href="https://s.click.aliexpress.com/e/_c3ZtFnwf" target="_blank"><img src="https://ae01.alicdn.com/kf/Sdef2a16cb4e54d9dad7a13c8556f0a65s.png_80x80.png" width="80" height="80" /></a><br>[**Shop BigTreeTech SKR Mainboard Deal →**](https://s.click.aliexpress.com/e/_c3ZtFnwf) |
