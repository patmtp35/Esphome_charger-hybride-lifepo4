# ⚡ Chargeur Hybride LiFePO₄ 24V – Victron + Emerson R48 (CANBUS) + DPS5020 (Modbus) + ESP32 (ESPHome)

#### Version Stable OK en Production V1.6.5 ==> Charger_Hybride_Ha_Victron_shelly.yaml

---

Version en cours de Test :

- 1.8.2 => ameliorations - securité et stabilité En cours de test 

- V 2.0 => on change de composant pour le emerson R48 par celui de Sebby et ces améliorations.
- 
## 🟦 1.6.6 version Autonome sans HA tout dans l'esp32
## 🟦 1.6.5 version simpliste mais OK
## 🟦 Version stable : **1.8.2 (2025)**
Nouvelle architecture sécurisée, modulaire, entièrement configurable via Substitutions.

⚠ IMPORTANT :
→ Installer un disjoncteur DC 63A entre DPS5020 et batterie.
→ Attention au risque de court-circuit : toujours câbler batterie isolée.

## 📌 Description générale
Ce projet pilote un système hybride de charge pour batterie LiFePO₄ 24V / 300Ah, utilisant :
- Victron SmartSolar
- Emerson / Vertiv R48 en CANBUS
- DPS5020 en Modbus UART
- ESP32 + ESPHome
- Lazy Limiter
- Home Assistant (optionnel)

## 🆕 Nouveautés majeures en 1.8.2
- Comparaison Victron directe
- Énergie réelle Wh / kWh
- Watchdogs améliorés
- Sécurité surintensité
- Reset Modbus automatique
- Charge bloquée → restart automatique
- Tous paramètres via substitutions

## 🔋 Énergie réelle
- Comptage Wh exact via R48 (I × V × rendement)
- Sensors Wh / kWh compatibles HA Energy
- Reset via switch
- Persistant EEPROM

## 🛡 Sécurités automatiques
- Surintensité >22A
- Surtension >29.2V
- Surchauffe >70°C
- Freeze Modbus
- Freeze CAN
- Reboot si HA indisponible
- Charge inactive >60s → restart

## 🧱 Matériel
ESP32, Victron SmartSolar, R48, DPS5020, Batterie LiFePO4 24V, Shelly EM.

## 🧩 Installation
1. Modifier substitutions
2. Importer fichier dans ESPHome
3. Flasher via USB

## 🙏 Crédits
syssi/esphome-dps  
jon7119/esphomeemerson-vertiv-r48  
IxioJo/esphome-emerson-vertiv-r48  
https://github.com/SeByDocKy/myESPhome

## 📜 Licence
MIT
