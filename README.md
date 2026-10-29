# Aziot IR Blaster (Type-C) - ESPHome Configuration

This repository contains the ESPHome configuration for the **Aziot IR Blaster (Type-C)**, based on the Beken BK72xx (t1-3s) chipset. 

This configuration provides a ready-to-use foundation for integrating the IR blaster into Home Assistant or any other smart home platform using ESPHome. It includes standard features like a captive portal, OTA updates, web server, and pre-mapped hardware pins for the IR receiver, transmitter, status LED, and physical button.

## Features

* **Beken BK72xx Support:** Fully configured for the `t1-3s` board.
* **IR Transmission & Reception:** Pre-mapped pins for the infrared transmitter and receiver.
* **Smart Home Integration:** Native Home Assistant API enabled.
* **Physical Controls:** Hardware reset/pairing button mapped and ready for automations.
* **Bluetooth Proxy (Optional):** Pre-written, commented-out blocks to easily enable ESPHome Bluetooth Proxy forwarding.
* **Secure:** Uses ESPHome's `secrets.yaml` structure so you never accidentally commit your Wi-Fi or API passwords.

## Hardware Pinout Reference

| Component | Pin | Notes |
| :--- | :--- | :--- |
| **Status LED** | `P24` | Inverted. Shared light entity. |
| **Hardware Button** | `P9` | Inverted, `INPUT_PULLUP`. |
| **IR Receiver (RX)** | `P26` | Inverted, `INPUT_PULLUP`. |
| **IR Transmitter (TX)** | `P6` | 50% Carrier duty. |

## Prerequisites

1. An installed instance of [ESPHome](https://esphome.io/) (Dashboard or CLI).
2. A way to initially flash the Beken chip (e.g., using [ltchiptool](https://github.com/libretiny-eu/ltchiptool) or via serial flasher, depending on your device's current firmware).

## Installation

1. Clone or download this repository.
2. Copy the `aziot_ir_blaster_typec_2026.yaml` file into your ESPHome configuration directory.
3. Ensure you have a `secrets.yaml` file in the same directory. You will need to define the following secrets:

```yaml
# Example secrets.yaml
wifi_ssid: "Your_WiFi_SSID"
wifi_password: "Your_WiFi_Password"
ap_password: "Fallback_AP_Password"
api_key: "Your_Generated_API_Key"
ota_password: "Your_OTA_Password"
```

4. Compile and install the firmware:
   * **First time:** Flash via serial connection.
   * **Subsequent updates:** Flash wirelessly via OTA.

## Customization

### Learning New IR Codes
By default, the `remote_receiver` is set to `dump: [raw]`. When you point a remote at the device and press a button, the raw IR codes will be printed in the ESPHome logs. 
* Once you have captured your desired codes, it is highly recommended to comment out `dump: [raw]` or change it to `dump: []` to prevent log spam from stray infrared noise.

### Adding Custom IR Commands
You can easily add switches or buttons to transmit specific IR codes by adding them to the YAML file. Check the [ESPHome Remote Transmitter documentation](https://esphome.io/components/remote_transmitter.html) for examples on transmitting standard protocols (NEC, Sony, etc.) or raw signals.
