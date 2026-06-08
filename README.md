# ESP32 Luxmeter - Photovoltaik-Planung

> Batteriebetriebener Lux-Sensor auf ESP32-C3 + VEML7700 fuer Langzeitmessung zur PV-Ertragsplanung.
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
3V3 → VIN / GND → GND / GPIO4 → SDA / GPIO5 → SCL
Batterie: GPIO0 ← Spannungsteiler 100k+100k ← LiPo+
```

## Quickstart

1. `esp32-lux.yaml` in Home Assistant hochladen
2. ESP32-C3 per USB flashen
3. Kalibrierung (Glasfaktor): ohne/mit Deckel messen
4. HA-Automation fuer Telegram-Akku-Warnung

## Entwickelt mit KI-Assistenz

- **VS Code + Zoo Code Extension**
- **Architect/Editor-Routing:** DeepSeek V4 Pro (Planung) + V4 Flash (Code, Debug)
- **GitHub MCP + Tavily MCP** fuer GitHub-Integration & Web-Recherche
- **PlattformIO 6.1.19 + ESPHome 2026.5.3**

## Lizenz

MIT
