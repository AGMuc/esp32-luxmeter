# Projektplanung

## Anwendungsfall

Lux-Werte an verschiedenen Balkon-Positionen messen, um PV-Ertrag zu planen.

## Kalibrierung (Glasfaktor)

1. Sensor OHNE Deckel → 30s messen
2. Deckel drauf → 30s messen
3. Faktor = Lux(ohne) / Lux(mit)
4. In `esp32-lux.yaml` eintragen → OTA-Update

## Kondensationsschutz

- Platine mit Plastik 70 einspruehen (VEML7700-Sensor abkleben!)
- Silica-Saeckchen ins Gehaeuse legen

## Akku-Warnung (Telegram)

ESP32 misst Batteriespannung via ADC → HA-Automation prueft Schwellwert → Telegram-Nachricht.

HA-Automation:
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
