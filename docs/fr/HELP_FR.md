# 📖 Avions dans le Ciel — Guide de l'Utilisateur

## Premiers Pas

### Ouvrir l'Application
Ouvrez `index.html` dans Chrome, Edge, Safari ou Firefox. Aucune installation nécessaire.

### Choisir Votre Position
Au premier lancement, le sélecteur de position apparaît :

- **📍 Ma Position** — utilise le GPS de votre appareil (plus précis, recommandé)
- **Boutons de villes** — touchez l'une des 10 villes : Paris, Londres, Dubaï, Istanbul, Casablanca, La Mecque, New York, Tokyo, Sydney, Singapour
- **Recherche** — tapez un nom de ville et sélectionnez le résultat

Votre position détermine quels avions apparaissent. L'appli suit les vols dans un rayon de ~200 km.

### Tutoriel de Bienvenue
Un parcours en 5 diapositives apparaît après le choix de position :
1. Introduction de bienvenue
2. Comment toucher les avions
3. La fonction de recherche par pays
4. Les cinq modes expliqués
5. Prêt au décollage !

---

## La Vue du Ciel

### Ce que Vous Voyez
- **Ciel animé** — le dégradé change selon l'heure à votre position
- **Étoiles** — scintillent la nuit, des étoiles filantes traversent occasionnellement
- **Soleil / Lune** — positionnés dans le ciel. Le soleil a un halo chaud. La lune a des cratères visibles
- **Nuages** — en couches pour la profondeur, dérivent lentement
- **Avions** — positionnés par coordonnées GPS réelles. La taille reflète l'altitude
- **Traînées de vapeur** — segments qui s'estompent derrière chaque avion
- **Anneaux de distance** — cercles en pointillés à 50, 100 et 150 km
- **Boussole** — coin inférieur droit, avec aiguille nord rouge

### Jour, Nuit et Crépuscule
Le ciel calcule automatiquement le lever et coucher du soleil :
- **Jour** — dégradé de ciel bleu
- **Crépuscule** — heure dorée avec dégradés mauve → rose → ambre → or
- **Nuit** — bleu profond à noir spatial, étoiles visibles, lune avec cratères

---

## Interagir avec les Avions

### Toucher un Avion
Touchez/cliquez sur un avion pour ouvrir le panneau d'informations :

- **Indicatif** — l'identifiant radio du vol (ex : « AFR1234 »)
- **Compagnie** — résolue depuis le préfixe (ex : « Air France »)
- **Altitude** — en mètres, avec comparaison amusante (« plus haut que l'Everest ! »)
- **Vitesse** — en km/h, avec comparaison (« plus rapide qu'un guépard ! »)
- **Nombre de Mach** — corrigé pour la température à l'altitude
- **Cap** — direction avec label (N, NE, E, etc.)
- **Vitesse verticale** — montée, descente ou croisière
- **Pays** — drapeau emoji, salutation native et 2 anecdotes
- **Distance** — à quelle distance l'avion se trouve de vous

### Fermer le Panneau
Touchez le ✕, touchez en dehors du panneau, ou appuyez sur `Esc`.

---

## Les Modes

### 🌤️ Mode Ciel (4 ans et +)
Expérience purement visuelle. Ciel magnifique, avions animés, texte minimal. Parfait pour les jeunes enfants.

### 📚 Mode Découvrir (6 ans et +)
Tout le mode Ciel plus : labels d'indicatifs, comparaisons amusantes, salutations en langues natives, anecdotes par pays.

### 📡 Mode Pro (10 ans et +)
Affichage radar complet : esthétique CRT vert-sur-noir, ligne de balayage avec rémanence, anneaux de portée, données par blip (indicatif, niveau de vol, distance).

### 🔬 Mode Expert (12 ans et +)
Tout visible sur le canevas plus : grille de coordonnées violette, consommation carburant estimée, probabilité de traînées, couche atmosphérique, données METAR, waypoints, export CSV.

### 🕌 Mode Héritage (Tous Âges)
Le ciel devient doré. Une chronologie de 9 savants de l'Âge d'Or islamique apparaît. Quand vous touchez un avion, le panneau montre des connexions en direct : « Les algorithmes d'Al-Khwarizmi calculent cette trajectoire ».

---

## Recherche et Filtre par Pays

### Ouvrir la Recherche
Touchez 🔍 en haut à droite ou appuyez sur `F` ou `/`.

### Filtrer
Tapez un nom de pays (ex : « France ») ou de compagnie (ex : « Air France »). L'appli met en valeur les avions correspondants avec un éclat doré et estompe les autres.

### Effacer
Touchez le ✕ dans la barre de recherche, appuyez sur `Esc`, ou touchez « Effacer le filtre ».

---

## Zoom et Déplacement

### Zoomer
- **Mobile** : geste de pincement (0.5× à 3×)
- **Bureau** : molette de souris
- **Clavier** : `+` pour zoomer, `-` pour dézoomer

### Déplacer
- **Mobile** : incliner le téléphone (gyroscope) ou glisser avec un doigt
- **Bureau** : cliquer et glisser

### Réinitialiser
- **Mobile** : double-tap
- **Bureau** : double-clic
- **Clavier** : `R`

---

## Audio

Activez/désactivez avec le bouton 🔇/🔊.

Quand activé :
- **Ambiance de vent** — fond continu qui s'adapte à la densité d'avions
- **Son de touche** — tonalité descendante courte
- **Changement de mode** — tonalité ascendante
- **Ping radar** — tonalité de balayage en entrant en mode Pro

Tous les sons sont synthétisés — aucun fichier audio nécessaire.

---

## Alertes de Proximité

Quand un avion passe à moins de **8 km** de votre position :
- Une barre dorée glisse du haut
- Affiche : compagnie, altitude et distance
- Vibration haptique subtile
- Disparaît après 5 secondes
- Pause de 30 secondes entre les alertes

---

## Récepteur SDR

### Connexion
1. Lancez `sdr_receiver.py` sur un ordinateur avec le dongle
2. Dans l'appli, touchez 📡 (en haut à droite)
3. Entrez l'URL du serveur (par défaut : `http://localhost:8090`)
4. Touchez **Connecter**

Voir `docs/SDR_GUIDE.md` pour les instructions complètes.

---

## Compagnon micro:bit

### Connexion
1. Flashez le micro:bit avec `microbit_makecode.js` ou `microbit_planes.py`
2. Touchez 🔌 (en haut à droite)
3. Sélectionnez votre micro:bit (Chrome/Edge uniquement)

Voir `docs/MICROBIT_GUIDE.md` pour les instructions complètes.

---

## Dépannage Rapide

| Problème | Solution |
|----------|----------|
| Pas d'avions | Attendez 10 secondes, ou appuyez sur `D` |
| « Position refusée » | Choisissez une ville à la place |
| Avions qui disparaissent | Limite API — attendez 10 secondes |
| Le ciel est noir | C'est la nuit à votre position ! |
| Pas de son | Touchez le bouton 🔇 |
| micro:bit ne se connecte pas | Utilisez Chrome ou Edge |
| SDR affiche « impossible d'atteindre » | Vérifiez que `sdr_receiver.py` tourne |
