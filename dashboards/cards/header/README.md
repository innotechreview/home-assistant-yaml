# 🏡 Configuration de Carte Empilée pour Météo et Énergie

Cette configuration YAML pour Home Assistant utilise la carte personnalisée `custom:stack-in-card` pour **empiler plusieurs cartes** (météo, prévisions horaires et graphiques d'énergie) sans bordures visibles entre elles. Cela permet de créer une vue intégrée et "lisse" sur votre tableau de bord.

---

## ⚙️ Prérequis

Pour utiliser cette configuration, vous devez avoir installé les cartes personnalisées suivantes via HACS :

1.  **`custom:stack-in-card`** : Pour empiler les cartes.
2.  **`custom:clock-weather-card`** : Pour l'affichage des conditions météo.
3.  **`custom:hourly-weather`** : Pour les prévisions horaires.
4.  **`custom:bubble-card`** : Utilisé pour le séparateur de section.
5.  **`custom:apexcharts-card`** : Pour l'affichage des graphiques d'énergie.
6.  **`card-mod`** : Essentiel pour appliquer le style `border: none;` et supprimer les bordures.

---

## ☀️ Section Météo

La section météo est composée de trois cartes pour offrir un aperçu complet et détaillé.

### 1. Météo du Jour (`custom:clock-weather-card`)

| Option | Description | Valeur Clé |
| :--- | :--- | :--- |
| `hide_today_section` | **Afficher** les conditions du jour. | `false` |
| `hide_forecast_section` | **Masquer** la prévision multi-jours (car elle est montrée dans une autre carte). | `true` |
| `entity` | Entité `weather` de votre fournisseur (ex: OpenWeatherMap, Météo-France, etc.). | `weather.forecast_maison` |
| `animated_icon` | Active les icônes météo animées. | `true` |
| `show_humidity` | Affiche le taux d'humidité. | `true` |
| `date_pattern` | Format de la date affichée (ex: lundi 17 octobre). | `EEEE d MMMM` |
| `aqi_sensor` | Capteur optionnel pour la qualité de l'air (AQI). | `sensor.air_quality_index` |
| `card_mod` | Suppression de la bordure pour s'intégrer dans le `stack-in-card`. | `border: none` |

### 2. Météo Horaire (12h) (`custom:hourly-weather`)

Cette carte affiche l'état du ciel heure par heure pour les 12 prochaines heures.

| Option | Description | Valeur Clé |
| :--- | :--- | :--- |
| `num_segments` | Nombre d'heures affichées. | `"12"` |
| `hide_temperatures` | **Masque** les températures pour un affichage plus minimaliste, ne montrant que l'état du ciel (soleil, nuages, pluie...). | `true` |
| `show_wind`, `show_date`... | Masque d'autres informations pour garder la carte compacte. | `"false"` |
| `colors` | Palette personnalisée pour les icônes/conditions météo. | Personnalisé |
| `card_mod` | Suppression de la bordure. | `border: none` |

### 3. Météo Compacte (Conditions Actuelles) (`custom:clock-weather-card`)

Une seconde instance pour une vue compacte des conditions actuelles (souvent la prévision multi-jours) en masquant la section "aujourd'hui".

| Option | Description | Valeur Clé |
| :--- | :--- | :--- |
| `hide_today_section` | **Masque** la section "aujourd'hui" pour n'afficher que la prévision ou la section compacte de la carte. | `1` |
| `card_mod` | Suppression de la bordure. | `border: none` |

---

## ⚡ Section Énergie

Cette section commence par un séparateur puis affiche les coûts d'énergie.

### 1. Séparateur de Section (`custom:bubble-card`)

Utilisé pour créer une ligne de séparation avec un titre et une icône.

| Option | Description | Valeur Clé |
| :--- | :--- | :--- |
| `card_type` | Type d'élément de la Bubble Card. | `separator` |
| `name` | Titre de la section. | `Consommation d'énergie` |
| `icon` | Icône associée. | `mdi:currency-usd` |

### 2. Graphique des Coûts Journaliers (`custom:apexcharts-card`)

Affiche l'évolution quotidienne du coût de l'électricité et de l'eau sur les 30 derniers jours.

| Option | Description | Valeur Clé |
| :--- | :--- | :--- |
| `graph_span` | Fenêtre totale des données affichées. | `30d` |
| `span` | Décalage pour afficher les **30 derniers jours** complets jusqu'à la veille. | `offset: "-30d"` |
| `series` | **Définition des données à tracer.** | |
| `statistics` | **Crucial** : Utilise le type `change` sur une période `day` pour afficher la **variation journalière** (le coût du jour) et non la valeur cumulée. | `type: change`, `period: day` |
| `apex_config` | Permet de régler l'apparence, notamment pour réduire la hauteur du graphique (`height: 150px`) et rendre la grille Y plus discrète. | Personnalisé |
| `card_mod` | Suppression de la bordure. | `border: none` |
