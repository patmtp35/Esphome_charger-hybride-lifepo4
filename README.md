# ⚡ Chargeur Hybride LiFePO₄ 24V – Victron SmartShunt + Emerson R48 (CAN) + DPS5020 (Modbus) + ESP32 (ESPHome)

### ✅ Version stable actuelle : **2.0**
### 🧪 Ancienne version stable : **1.6.5**

---

# 🧪 Versions

### 🟢 2.0 (2025) – Version hybride STABLE (SmartShunt intégré)
Version de référence du projet.  
Ajout du **Victron SmartShunt 500A comme source de vérité batterie**, logique Victron consolidée, fallback sécurisé et architecture robuste.

### 🟦 1.9.1-H – Version hybride intermédiaire (dépréciée)
Version de transition avant l’intégration complète du SmartShunt.

### 🟩 1.6.5 – Version simplifiée mais stable (production)
Fonctionnelle sans SmartShunt, logique plus simple.

### 🟪 2.1-H – En développement
Migration prévue vers un composant R48 unifié (Sebby / refactor CAN).

---

# 🚀 Nouveautés majeures de la version 2.0

## 🧭 1. Victron = source de vérité
- **Victron SmartShunt 500A** = vérité batterie  
  - Tension  
  - Courant  
  - Puissance (signée : + charge / – décharge)  
  - Énergie réelle  
- **Victron SmartSolar** = état de charge  
  - bulk / absorption / float  

Le chargeur n’est autorisé à fonctionner **que si Victron est en mode charge** (hors mode forcé).

---

## 🔒 2. Modbus DPS sécurisé
- Anti-spam Modbus (délai mini entre commandes)  
- Rampe de courant progressive (Lazy Limiter)  
- Watchdog freeze intelligent  
- Reset automatique Modbus  
- Limites tension / courant strictes  

---

## ⚙️ 3. Séquence Emerson R48 robuste
- Reset AC court au démarrage  
- Précharge DPS  
- Configuration automatique :
  - 48 V  
  - 30 % DC  
  - 6 A AC  
- Activation conditionnée par Victron  
- Sécurité nuit (pas de démarrage automatique)

---

## ⚡ 4. Lazy Limiter optimisé (surplus PV)
- Pilotage via Linky / Shelly / smartmeter HA  
- Hystérésis :
  - ON ≥ 30 W  
  - OFF ≤ 10 W  
- Rampe progressive du courant  
- Pilotage fluide et stable du DPS  

---

## 🛡 5. Watchdogs intelligents
- Freeze Modbus DPS  
- Freeze CAN Emerson R48  
- Charge bloquée (courant demandé sans puissance réelle)  
- Surtension batterie :
  - Alerte : 29.0 V  
  - Coupure : 29.2 V  
- Surintensité > 22 A  
- Surchauffe > 70 °C  
- Gestion ventilateur R48 (60 / 50 °C)  

---

## 🔋 6. Énergie batterie fiable
- **Énergie réelle batterie via SmartShunt (référence)**  
- Énergie estimée côté R48 (I × V × rendement DPS)  
- Capteurs Wh / kWh  
- Valeurs persistantes (EEPROM)  
- Reset manuel via switch  

Les puissances négatives (décharge) **ne sont jamais comptées comme charge**, conformément à la convention Victron.

---

## 🔁 7. Fallback & modes dégradés
- Perte SmartShunt → bascule automatique en mode DEGRADED  
- Utilisation des mesures DPS si disponibles  
- Absence totale de mesure fiable → **SAFE MODE (DPS OFF)**  
- Aucun redémarrage dangereux automatique  


---

# 🧱 Matériel requis
- ESP32 DevKit  
- Emerson / Vertiv R48-3000 (CAN MCP2515 8 MHz)  
- DPS5020 (Modbus RTU UART)  
- Victron SmartShunt 500A  
- Victron SmartSolar  
- Batterie LiFePO₄ 24V (ex: 300 Ah)  
- Linky Téléinfo / Shelly EM / autre smartmeter HA  

⚠️ **Important** :  
Blinder le câble UART ESP32 ↔ DPS ou ajouter une **ferrite** (obligatoire en environnement bruité).

---

# 🛠 Installation
1. Adapter les `substitutions` (pins, IP, seuils)  
2. Importer le YAML dans ESPHome  
3. Flasher l’ESP32 via USB  
4. Ajouter les entités dans Home Assistant  

---

# ⚠️ Sécurité
- Disjoncteur DC **63 A minimum** entre DPS et batterie  
- Toujours câbler **batterie déconnectée**  
- Ventilation obligatoire (R48 + DPS)  
- Mode forcé = Victron ignoré → **usage expert uniquement**  

⚠️ Projet destiné à des utilisateurs avancés.  
Courants DC élevés = danger réel en cas d’erreur.

---

# 🙏 Crédits
- syssi / esphome-dps  
- jon7119 / esphomeemerson-vertiv-r48  
- IxioJo / esphome-emerson-vertiv-r48  
- SeByDocKy / myESPhome  

---

# 📜 Licence
MIT
---

# 📌 Architecture
