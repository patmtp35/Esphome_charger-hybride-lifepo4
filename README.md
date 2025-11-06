# ⚡ Chargeur Hybride LiFePO₄ 24V – Victron + Emerson R48 + DPS5020 + ESP32 (ESPHome)

## 📌 Description générale

Ce projet permet de piloter un système de charge hybride pour batterie **LiFePO₄ 24V / 300Ah** en s'appuyant sur :
- Le **chargeur solaire Victron** comme source de vérité des phases de charge (Bulk, Absorption, Float),
- Une alimentation **Emerson/Vertiv R48** (48V) pilotée via **CANBUS**,
- Un convertisseur **DPS5020** contrôlé via **Modbus UART**,
- Un **ESP32** sous **ESPHome**, connecté à Home Assistant.

🎯 **Objectif :** exploiter le surplus photovoltaïque et automatiser la charge de la batterie tout en garantissant la sécurité, l'efficacité et la compatibilité avec Victron.

---

## ⚙️ Fonctionnalités principales

✅ Pilotage par Victron :  
- Lecture du mode de charge Victron (`bulk`, `absorption`, `float`) via Home Assistant.  
- Décalage automatique de tension : `Tension_DPS = Tension_Victron - 0.20V`.

✅ Démarrage / arrêt intelligents :  
- Si Victron est en charge → activation R48 AC + DPS5020.  
- Si Victron est OFF / IDLE / NIGHT / FAULT → R48 AC OFF + DPS OFF.  
- Mode **forcé** possible pour ignorer Victron.

✅ Utilisation du surplus photovoltaïque :  
- Mesure via `sensor.cptlinkyshe_power`.  
- Lazy Limiter → convertit les Watts disponibles en Ampères de charge (max 19.5A / 500W).

✅ Sécurités intégrées :  
- Surtension batterie (>29.2V) → coupure immédiate DPS.  
- Surintensité (>22A) → arrêt + redémarrage automatique.  
- Surchauffe Emerson (>70°C) → DC OFF + DPS OFF.  
- Watchdogs Modbus (DPS), CAN (R48), API/Wi-Fi.  
- Reboot ESP32 si Home Assistant injoignable >10 min.

---

## 🧱 Architecture matérielle

| Élément | Rôle |
|---------|------|
| ESP32 | Contrôleur principal (ESPHome) |
| Victron SmartSolar | Source des phases de charge |
| Emerson/Vertiv R48 | Alimentation AC → 48V, pilotée via CANBUS |
| DPS5020 | DC/DC 48V → 24V, piloté via Modbus |
| Batterie LiFePO₄ 24V | Stockage énergie |
| Shelly EM ou compteur | Mesure du surplus photovoltaïque |

📎 Schémas disponibles dans `/docs/shema.png` et `/docs/flow.png`


### ✅ 3. Flash
- Ouvrir ESPHome → **Install**  
- Sélectionner **Plug into this computer**  
- Flasher l'ESP32 via USB

---

## 🛡 Sécurités automatiques

| Protection | Action |
|------------|--------|
| Surtension (>29.2V) | DPS OFF immédiat |
| Surintensité (>22A) | DPS OFF + reprise si courant <5A |
| Température R48 (>70°C) | DC OFF + DPS OFF |
| Modbus inactif | Reset DPS ou redémarrage séquence |
| CAN R48 silencieux | Reset DC court |
| Home Assistant absent >10 min | Reboot ESP |
| Charge active mais 0W | Redémarrage DPS après 60s |

---

## 🙏 Crédits

Merci aux projets suivants :  
- https://github.com/syssi/esphome-dps  
- https://github.com/jon7119/esphomeemerson-vertiv-r48  
- https://github.com/IxioJo/esphome-emerson-vertiv-r48  

---

## 📜 Licence

Ce projet est sous licence **MIT**.  
Vous êtes libres de l'utiliser, le modifier et le partager (avec mention de l'auteur).



