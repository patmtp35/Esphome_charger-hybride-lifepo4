# ⚡ Chargeur Hybride LiFePO₄ 24V – Victron + Emerson R48 (CANBUS) + DPS5020 (Modbus) + ESP32 (ESPHome)

### Version stable actuelle : **1.6.5**
### Version avancée en test : **1.9.1-H (Hybride)**

---

# 🧪 Versions en cours

### 🟧 1.9.1-H (2025) – Version hybride optimisée (EN TEST)
Fusion entre la stabilité de la 1.6.5 et la protection complète de la 1.8.x  
+ Correctifs Modbus, watchdogs avancés, logique Victron améliorée, compatibilité HA totale.
+ ne pas oublier de blindé ou bloc de ferite pour le cable de com esp32-dps

### 🟦 1.8.x – Améliorations sécurité (bus instable sur longues sessions)
### 🟩 1.6.6 – Version autonome (sans Home Assistant)
### 🟦 1.6.5 – Version simplifiée mais stable (production)
### 🟪 2.1-H – En développement (migration vers composant Sebby R48)

---

# 🚀 Nouveautés majeures de la version 1.9.1-H

## 🧭 1. Victron comme source de vérité
Le mode Victron pilote :  
- l’autorisation de charge  
- la tension cible du DPS  
- l’activation R48 AC  
- l’activation du DPS  

## 🔒 2. Modbus DPS sécurisé
- Anti-spam (50–300 ms)  
- Rampe de courant (Lazy Limiter)  
- Watchdog freeze intelligent  
- Reset automatique  
- Limites tension + courant

## ⚙️ 3. Séquence R48 robuste
- Reset AC court  
- Précharge DPS  
- Configuration auto 48V / 30% / 6A  
- Démarrage sécurisé selon Victron  
- Sécurité nuit

## ⚡ 4. Lazy Limiter optimisé
- Déclenchement Linky / surplus PV  
- Hystérésis 30W / 10W  
- Rampe progressive  
- Pilotage fluide du courant

## 🛡 5. Watchdogs intelligents
- Modbus freeze (réel)  
- CAN freeze  
- Charge bloquée  
- Surtension 29.0 / 29.2V  
- Surintensité >22A  
- Surchauffe >70°C  
- Température fan 60/50°C

## 🔋 6. Énergie réelle batterie
- Mesure côté R48 (I×V×efficiency)  
- Sensors Wh / kWh  
- Persistant EEPROM  
- Reset via switch  

---

# 📌 Architecture
AC → Emerson R48 (CAN) → DPS5020 (Modbus) → Batterie LiFePO₄  
ESP32 + ESPHome ← Home Assistant + Victron

---

# 🧱 Matériel requis
- ESP32 DevKit  
- Emerson / Vertiv R48-3000 (CAN MCP2515 8 MHz)  
- DPS5020 (Modbus UART)  
- Victron SmartSolar  
- Batterie LiFePO₄ 24V 300Ah  
- Shelly EM ou Linky Téléinfo  

---

# 🛠 Installation
1. Modifier les substitutions  
2. Importer dans ESPHome  
3. Flasher via USB  
4. Ajouter les entités HA

---

# ⚠️ Sécurité
- Disjoncteur DC **63A** obligatoire entre DPS et batterie  
- Toujours câbler batterie déconnectée  
- Ventilation obligatoire (R48 + DPS)  
- Mode Forcé = ignorer Victron → usage prudent  

---

# 🙏 Crédits
- syssi/esphome-dps  
- jon7119/esphomeemerson-vertiv-r48  
- IxioJo/esphome-emerson-vertiv-r48  
- SeByDocKy/myESPhome  

---

# 📜 Licence
MIT
