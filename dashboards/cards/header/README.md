# ðŸ§­ Dashboard MÃ©tÃ©o & Ã‰nergie pour Home Assistant

Ce tableau de bord Home Assistant affiche :

- ðŸŒ¤ï¸ Les **conditions mÃ©tÃ©o actuelles** (avec AQI si disponible)  
- ðŸ•’ La **tendance horaire** sur 12 heures  
- âš¡ Une section **â€œConsommation dâ€™Ã©nergieâ€** montrant la **variation quotidienne de coÃ»t** dâ€™Ã©lectricitÃ© et dâ€™eau sur les 30 derniers jours  

Design : cartes empilÃ©es sans bordures pour un rendu propre et compact.

---

## ðŸ§° PrÃ©requis

Installer les cartes personnalisÃ©es suivantes (idÃ©alement via **HACS**) :

| Carte / Plugin | UtilitÃ© |
|----------------|----------|
| `stack-in-card` | Empiler plusieurs cartes sans bordure |
| `clock-weather-card` | Afficher la mÃ©tÃ©o et lâ€™heure |
| `hourly-weather` | Afficher la mÃ©tÃ©o horaire |
| `bubble-card` | CrÃ©er des sÃ©parateurs et titres stylÃ©s |
| `apexcharts-card` | Afficher des graphiques (coÃ»ts, consommation, etc.) |
| `card-mod` | Personnaliser les styles (bordures, marges, etc.) |

> ðŸ§© Si HACS ne les ajoute pas automatiquement, vÃ©rifie dans **ParamÃ¨tres â†’ Tableaux de bord â†’ Ressources** que les ressources sont bien dÃ©clarÃ©es.

---

## ðŸŒ¡ï¸ EntitÃ©s attendues

| EntitÃ© | Description |
|--------|-------------|
| `weather.forecast_maison` | EntitÃ© mÃ©tÃ©o principale |
| `sensor.air_quality_index` *(optionnel)* | Indice de qualitÃ© de lâ€™air |
| `sensor.compteur_d_energie_linky_base_cost` | CoÃ»t cumulÃ© de lâ€™Ã©lectricitÃ© |
| `sensor.veolia_last_index_cost` | CoÃ»t cumulÃ© de lâ€™eau |

> Si tu nâ€™as pas de capteurs de coÃ»t, tu peux utiliser des capteurs dâ€™index (kWh / mÂ³) et garder le calcul `statistics: change / period: day` pour obtenir les variations journaliÃ¨res.

---

## ðŸ§± Installation

1. Installe les cartes via **HACS**.  
2. Ouvre ton **tableau de bord Home Assistant**.  
3. Clique sur **Modifier le tableau de bord â†’ Ajouter une carte â†’ Carte manuelle**.  
4. Copie le contenu du fichier [`dashboard.yaml`](./dashboard.yaml).  
5. Adapte les entitÃ©s si nÃ©cessaire.  
6. Enregistre âœ…

---

## ðŸ“Š Fonctionnement du graphique

Les graphiques utilisent :

```yaml
statistics:
  type: change
  period: day
```

Cela permet dâ€™afficher **la variation quotidienne** dâ€™un capteur cumulatif (index ou coÃ»t).  
Ainsi, mÃªme si ton capteur mesure un total, le graphique montre le **coÃ»t ou la consommation journaliÃ¨re**.

---

## âš™ï¸ Personnalisation

| Ã‰lÃ©ment | ParamÃ¨tre Ã  modifier | Effet |
|----------|----------------------|--------|
| Nombre dâ€™heures mÃ©tÃ©o | `num_segments` | DÃ©finit la durÃ©e (12h, 24h, etc.) |
| Afficher les tempÃ©ratures | `hide_temperatures: false` | Affiche les valeurs |
| Afficher la pluie | `show_precipitation_probability: true` | Montre la probabilitÃ© de prÃ©cipitation |
| Palette mÃ©tÃ©o | Bloc `colors:` | Change les couleurs selon la condition |
| Couleur des courbes | `color:` dans chaque sÃ©rie ApexCharts | Personnalise le graphique |

---

## ðŸš¨ DÃ©pannage

| ProblÃ¨me | Solution |
|-----------|-----------|
| âŒ Carte introuvable | VÃ©rifie quâ€™elle est bien installÃ©e via HACS |
| ðŸŒ«ï¸ AQI non affichÃ© | Supprime `aqi_sensor` ou corrige lâ€™entitÃ© |
| ðŸ“‰ Graphique vide | VÃ©rifie que les capteurs renvoient des valeurs numÃ©riques |
| ðŸ“Š Courbes plates | Active lâ€™historique / statistiques dans Home Assistant |
| ðŸ“ Dossier vide sur GitHub | Ajoute un fichier `.gitkeep` pour le conserver |

---

## ðŸ™Œ CrÃ©dits

Ce tableau de bord utilise des cartes crÃ©Ã©es par la communautÃ© Home Assistant :

- [`stack-in-card`](https://github.com/custom-cards/stack-in-card)  
- [`clock-weather-card`](https://github.com/ABeltramo/clock-weather-card)  
- [`hourly-weather`](https://github.com/decompil3d/lovelace-hourly-weather)  
- [`bubble-card`](https://github.com/Clooos/Bubble-Card)  
- [`apexcharts-card`](https://github.com/RomRider/apexcharts-card)  
- [`card-mod`](https://github.com/thomasloven/lovelace-card-mod)

---

## ðŸª„ Exemple de rendu

> *(Ajoute ici une capture dâ€™Ã©cran de ton tableau de bord une fois affichÃ© dans Home Assistant)*

---

## ðŸ“ Structure recommandÃ©e

```
dashboard/
â”œâ”€â”€ dashboard.yaml      # Le code Lovelace complet
â””â”€â”€ README.md           # Ce fichier
```

---

## ðŸ§‘â€ðŸ’» Auteur

CrÃ©Ã© et partagÃ© par [@Innotechreview](https://www.youtube.com/@innotechreview)  
ChaÃ®ne YouTube dÃ©diÃ©e Ã  la domotique, Home Assistant, Zigbee2MQTT et Node-RED ðŸ”Œ

---