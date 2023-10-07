# ✈️ Avions dans le Ciel — v1.0

**Un traqueur de vols en temps réel conçu pour les enfants, qui transforme le ciel en salle de classe interactive.**

Regardez de vrais avions voler au-dessus de votre tête sur un ciel animé. Touchez un avion pour découvrir sa compagnie, son pays, son altitude, sa vitesse — et des anecdotes amusantes. Cinq modes progressifs accompagnent l'apprenant, d'un enfant de 4 ans qui touche des avions à un ado de 14 ans qui lit les données METAR. Compagnon micro:bit et récepteur SDR optionnels pour le STEM pratique.

Construit en **un seul fichier HTML** — pas de serveur, pas d'outils de build, pas de frameworks, zéro dépendance.

---

## Démarrage Rapide

1. Ouvrir `index.html` dans un navigateur moderne
2. Autoriser l'accès à la localisation (ou choisir une ville)
3. Les avions apparaissent en temps réel. Touchez-en un !

> **Pas d'avions ?** L'appli active automatiquement le Mode Démo avec des vols simulés après 2 échecs API. Appuyez sur `D` pour basculer manuellement.

---

## Cinq Modes Progressifs

| Mode | Âges | Ce qu'il montre |
|------|------|-----------------|
| 🌤️ **Ciel** | 4+ | Ciel animé avec parallaxe, jour/nuit/crépuscule, nuages en couches, cratères lunaires, halos solaires. Touchez un avion pour voir son drapeau et salutation. |
| 📚 **Découvrir** | 6+ | Comparaisons d'altitude et vitesse (« plus haut que l'Everest ! »), salutations culturelles en langues natives, anecdotes par pays avec emoji. |
| 📡 **Pro** | 10+ | Radar complet avec balayage rémanent, flèches de cap, distances, alertes SQUAWK, panneau NOTAM. |
| 🔬 **Expert** | 12+ | Météo METAR, couches atmosphériques, consommation carburant, nombre de Mach, prédiction de traînées, grille de coordonnées, waypoints, export CSV. |
| 🕌 **Héritage** | Tous | Chronologie des savants de l'Âge d'Or islamique — 9 savants liés aux mathématiques du vol en temps réel. |

Changez de mode avec les pilules en haut ou les touches `1`–`5`.

---

## Neuf Formes d'Avions

Touchez ✏️ ou appuyez sur `S` pour changer :

| Forme | Icône | Description |
|-------|-------|-------------|
| Avion de ligne | ✈️ | Jet détaillé avec fuselage dégradé, ailes en flèche, moteurs, hublots, feux de navigation |
| Chasseur | 🛩️ | Aile delta avec canards, dérives jumelles, bulle de cockpit, lueur de postcombustion |
| Hélice | 🛫 | Avion à hélice classique avec ailes droites, hélice 3 pales animée |
| Hélicoptère | 🚁 | Corps arrondi, rotors principal et de queue animés, patins d'atterrissage |
| Avion en papier | 📄 | Pliage origami avec ligne de pli et ombre subtile |
| Fusée | 🚀 | Style rétro avec cône, ailettes, hublot, flamme bicolore vacillante |
| Oiseau | 🐦 | Ailes battantes animées, plumes de queue, bec, œil avec pupille |
| OVNI | 🛸 | Soucoupe volante avec dôme, 8 lumières tournantes, rayon tracteur occasionnel |
| Étoile | ⭐ | Étoile à 5 branches tournante avec lueur radiale, pulsation, étincelles |

---

## Fonctionnalités Principales

### Sources de Données
- **API OpenSky Network** — par défaut, aucune configuration requise
- **Récepteur SDR** — ADS-B en direct depuis un dongle RTL-SDR (voir `docs/SDR_GUIDE.md`)
- **Mode Démo** — vols simulés, s'active si l'API est inaccessible

### Visuel
- **Lever/coucher de soleil** calculé depuis le GPS + déclinaison solaire
- **Dégradés crépusculaires** — mauve → rose → ambre → or
- **Nuages en couches** avec bouffées secondaires volumétriques
- **Lune** avec cratères et halo / **Soleil** avec halo et reflet
- **Étoiles filantes** la nuit avec traînées en dégradé
- **Anneaux de distance** à 50/100/150 km
- **Boussole améliorée** avec labels cardinaux, aiguilles rouge/blanc

### Interaction
- **Recherche par pays** — 🔍 ou touche `F`. Tapez un pays ou une compagnie
- **Pinch-to-zoom** — pincement mobile ou molette, 0.5× à 3×
- **Double-tap/clic** réinitialise le zoom et le déplacement
- **Alerte de proximité** — notification dorée quand un avion passe à moins de 8 km
- **Retour haptique** au toucher et aux alertes
- **Parallaxe gyroscopique** — inclinez votre téléphone pour regarder autour

### Audio
- **Ambiance de vent** qui s'adapte au nombre d'avions
- **Son de touche** — onde sinusoïdale descendante
- **Changement de mode** — onde triangulaire ascendante
- **Ping radar** — en entrant en mode Pro

### Données
- **50 pays** avec drapeau, salutation et 2 anecdotes chacun
- **83 compagnies** reconnues par préfixe d'indicatif OACI
- **50+ plages hexadécimales OACI** pour la détection de pays depuis l'ADS-B brut
- **10 villes** dans le sélecteur (Paris, Londres, Dubaï, Istanbul, Casablanca, La Mecque, New York, Tokyo, Sydney, Singapour)

### Mode Héritage (Âge d'Or Islamique)
- 9 savants : Al-Khwarizmi, Abbas ibn Firnas, Ibn al-Haytham, Al-Battani, Al-Biruni, Al-Jazari, Al-Idrisi, Al-Zahrawi, Fatima al-Fihri
- Connexions en temps réel avec les mathématiques du vol
- Chronologie interactive avec fiches de savants
- Notifications dorées reliant savants et données en direct

---

## Compagnons Matériels

### 🔌 micro:bit (voir `docs/MICROBIT_GUIDE.md`)
Connectez un BBC micro:bit via Web Bluetooth pour une tour de contrôle physique : radar LED, compteur d'avions, pointeur de boussole, alertes avec buzzer.

### 📡 Récepteur SDR (voir `docs/SDR_GUIDE.md`)
Recevez de l'ADS-B en direct avec un dongle RTL-SDR (~25€). Aucun internet requis. Trois backends : rtl_adsb, dump1090, SBS/BaseStation. Guide de déploiement Raspberry Pi inclus.

---

## Raccourcis Clavier

| Touche | Action |
|--------|--------|
| `1`–`5` | Changer de mode |
| `S` | Changer la forme |
| `F` ou `/` | Recherche par pays |
| `D` | Mode démo |
| `+` / `-` | Zoom + / − |
| `R` | Réinitialiser le zoom |
| `Esc` | Fermer les panneaux |

---

## Spécifications Techniques

| Métrique | Valeur |
|----------|--------|
| Fichier | Un seul `index.html` |
| Taille | ~183 Ko |
| Lignes | ~2 565 |
| Dépendances | Aucune |
| APIs | OpenSky Network, Nominatim, Google Fonts |
| Rendu | Canvas 2D à DPI natif |
| Audio | Web Audio API (synthétisé) |
| Bluetooth | Web Bluetooth API (micro:bit) |
| Langues | Anglais, Français, Arabe (RTL) |

---

## Crédits

- Données de vol : [OpenSky Network](https://opensky-network.org/)
- Géocodage : [Nominatim / OpenStreetMap](https://nominatim.org/)
- Décodage ADS-B : [pyModeS](https://github.com/junzis/pyModeS)
- Recherche sur l'Âge d'Or islamique : sources académiques diverses
- Police : Inter, Noto Kufi Arabic (Google Fonts)

---

## Licence

Licence MIT — voir fichier `LICENSE`. Libre pour usage personnel, éducatif et commercial.

---

*Construit avec amour pour les enfants curieux qui regardent le ciel et se demandent où vont ces avions.* ✈️
