# ESP32 Luxmeter - Photovoltaik-Planung

> Batteriebetriebener Lux-Sensor auf ESP32-C3 + VEML7700 für Langzeitmessung zur PV-Ertragsplanung.
> ESPHome + Home Assistant Integration. Akku-Warnung via Telegram.

## Komponenten

| Komponente | Spezifikation |
|---|---|
| Mikrocontroller | ESP32-C3 SuperMini (RISC-V, WiFi) |
| Lichtsensor | VEML7700 (I2C, 0-120k lux, 0x10) |
| Akku | 1500mAh LiPo, PH2 |
| Gehaeuse | IP67 transparent |

## Pinbelegung

```
ESP32-C3 → VEML7700
────────────────
3V3     → VIN
GND     → GND
GPIO4   → SDA
GPIO5   → SCL

Batterie ADC:
GPIO0 ← Spannungsteiler 100k+100k ← LiPo+
```

## Laufzeit

- 15-Minuten-Intervall: ca. 66 Tage
- 5-Minuten-Intervall: ca. 34 Tage

## Quickstart

1. ESPHome-YAML (`esp32-lux.yaml`) hochladen
2. Per USB flashen
3. Kalibrierung (Glasfaktor): Sensor ohne/mit Deckel messen
4. HA-Automation fuer Telegram-Akku-Warnung aktivieren

## HA-Automation (Telegram-Warnung)

```yaml
- alias: "ESP32-Lux Akku leer"
  trigger:
    - platform: numeric_state
      entity_id: sensor.esp32_lux_batteriespannung
      below: 3.5
  action:
    - service: telegram_bot.send_message
      data:
        message: "ESP32-Lux Akku bei {{ states('sensor.esp32_lux_batteriespannung') }}V!"
```

## Lizenz

MIT