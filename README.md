# ⚡ Régul'Elec — Diagnostic & Analyse de régulation du chauffage électrique

[![Licence: MIT](https://img.shields.io/badge/Licence-MIT-blue.svg)](LICENSE)
[![Zero Backend](https://img.shields.io/badge/Backend-Aucun%20(100%25%20Local)-brightgreen.svg)]()
[![JavaScript](https://img.shields.io/badge/Techno-HTML5%20%2F%20Vanilla%20JS-yellow.svg)]()

> **Régul'Elec** est un outil web léger, autonome et 100 % exécuté côté client, conçu pour analyser les courbes de charge électriques horaires (exports CSV Enedis) et diagnostiquer la qualité de régulation du chauffage électrique (et de la climatisation).

Il permet d'identifier immédiatement les défauts de programmation : **absence de réduit nocturne**, **chauffe continue le week-end**, **talon de veille excessif**, et calcule le **gisement d'économies d'énergie (€ et kWh)** réalisable par une intermittence optimisée.

---

## 🎯 Fonctionnalités principales

- 🔒 **100 % Local** : Aucune donnée n'est transmise à un serveur externe. Tout le traitement se fait directement depuis le navigateur web.
- 📈 **Profils 24h comparatifs** :
  - Visualisation superposée des profils moyens horaires : Semaine Hiver (Lun-Ven), Week-end Hiver (Sam-Dim), Semaine Été, et courbe cumulée 7j/7.
  - Identification visuelle immédiate de l'intermittence (ou de son absence).
- 🧩 **Décomposition des usages & Bilan mensuel** :
  - Séparation rigoureuse de la consommation en 3 ou 4 composantes :
    1. 🟦 **Talon permanent de veille** (usages incompressibles 24h/24).
    2. 🟧 **Électricité spécifique** (activité des usagers, bureautique, éclairage — modélisée sur la période hors chauffe / mi-saison et reconduite en hiver).
    3. 🟥 **Chauffage électrique estimé** (surplus thermique hivernal).
    4. ❄️ **Climatisation estivale** (optionnelle, si le bâtiment est climatisé l'été).
  - Graphique empilé mensuel avec infobulles interactives et tableau de synthèse annuel.
- 🎛️ **Simulateur d'économies & Réduit** :
  - Définition libre des plages horaires de réduit de nuit.
  - Paramétrage du delta de température d'abaissement (°C) et de l'occupation le week-end (samedi / dimanche).
  - Estimation instantanée des gains financiers (€/an) et énergétiques (kWh/an et % de la facture).
- 🗺️ **Heatmap 24h × 365 jours & Chronocourbes** :
  - Vue cartographique thermique pour repérer en un coup d'œil les allumages intempestifs, oublis pendant les vacances ou dérives de régulation.
- ⚙️ **Paramétrage dynamique en direct** :
  - Modification à la volée des dates de saison de chauffe, de période d'été et de climatisation.
  - Prix de l'électricité (€/kWh) personnalisable.

---

## 🚀 Utilisation rapide

### 1. Téléchargement ou clonage
Cet outil ne nécessite aucune installation, aucun environnement Node.js, ni serveur web :

```bash
git clone https://github.com/votre-compte/regulelec.git
cd regulelec
```

### 2. Lancement
Ouvrez simplement le fichier `analyse_regulation_chauffage.html` dans n'importe quel navigateur moderne

### 3. Analyse d'une courbe de charge
1. Glissez-déposez un export horaire annuel Enedis au format `.csv` (séparateur point-virgule `;`).
2. *Ou cliquez sur le bouton **« Charger un exemple »** pour explorer l'outil avec le jeu de données fourni (`export conso 2025.csv`).*
3. Consultez directement les indicateurs, les graphiques et le simulateur d'économies.

---

## 📥 Format du fichier Enedis attendu

L'application accepte nativement les exports de courbe de charge horaire issus du portail client Enedis :
- **Format** : CSV (`.csv`)
- **Séparateur** : Point-virgule (`;`)
- **Colonnes principales** :
  - `Horodate` : Format ISO (`YYYY-MM-DDTHH:mm:ssZ` ou `YYYY-MM-DD HH:mm:ss`)
  - `Valeur` : Puissance moyenne appelée en kW ou énergie horaire en kWh
- Les métadonnées d'en-tête Enedis (adresse, PRM, etc.) sont ignorées automatiquement par l'analyseur.

---

## 📐 Méthodologie physique de l'outil

1. **Talon permanent de veille ($P_{\text{talon}}$)** :
   - Évalué à partir du 10ᵉ percentile ($P_{10}$) de nuit en période estivale (hors chauffage et hors climatisation). Il reflète les consommations minimales incompressibles (veilles, serveurs, ventilation, sécurité).
2. **Électricité spécifique d'activité ($P_{\text{spec}}$)** :
   - Isolée hors période de chauffe pendant les heures diurnes ouvrées et week-ends, puis reconduite pour chaque heure d'hiver afin de ne pas surévaluer le chauffage.
3. **Surpuissance nocturne d'hiver** :
   - La différence entre la puissance de nuit en hiver et le talon d'été mesure (avec une haute probabilité) le maintien de température d'un bâtiment inoccupé la nuit.
4. **Calcul d'économies du simulateur** :
   - Repose sur la règle physique reconnue par l'ADEME : **1 °C d'abaissement de consigne génère environ 7 % d'économie** sur la part de chauffage nette pendant les plages d'inoccupation configurées.

---

## 🤖 Projet personnel

- Ce projet est un **projet personnel** développé par **Nathan Château** ([chateaunathan@proton.me](mailto:chateaunathan@proton.me)).

---

 ## Utilisation de l'IA
 
 - **Mention IA** : Ce projet a été développé en utilisant une IA générative. L'utilisation de l'IA a permis de créer rapidement cet outil libre, utile, léger et sans serveur.
---

## 📄 Licence

Ce projet est distribué sous licence libre **MIT**. Vous êtes libre de l'utiliser, l'adapter et l'intégrer pour vos propres diagnostics énergétiques.
