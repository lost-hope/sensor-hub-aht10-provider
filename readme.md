# AHT10/AHT20 Sensor Provider

A [Sensor Hub](../sensor-hub/readme.md) provider usermod for the Aosong
AHT10/AHT20 - registers `aht10_temperature` and `aht10_humidity` with the
hub by default, which then handles MQTT, Home Assistant discovery, the
JSON API and the Info tab.

## Hardware

Wire SDA/SCL to the I2C pins configured on WLED's own **Config > LED
Preferences** page (shared across all I2C usermods, fixed sensor address
`0x38`). This usermod does not call `Wire.begin()` itself. Retries
`begin()` every 10s if the sensor isn't found; after 3 consecutive failed
reads both sensors are marked unavailable in Home Assistant, after 10 it
re-attempts `begin()`.

## Usage

Self-contained out-of-tree usermod (see `library.json` for its
`adafruit/Adafruit AHTX0` dependency). Add it to `custom_usermods` next to
the [Sensor Hub](../sensor-hub/readme.md) itself.

## Usermod Settings

| Setting | Default | Description |
|---|---|---|
| Enabled | on | Master on/off switch (also auto-disabled if I2C pins aren't configured) |
| Check interval | 30s | How often the sensor is read |
| Name prefix | `aht10` | Sensor names become `<prefix>_temperature/_humidity` - must be unique across every provider registered with the hub |
| Precision | 1 | Decimal places published for both readings |
