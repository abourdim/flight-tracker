# 🔌 Compagnon micro:bit — Guide d'Installation

## Ce Dont Vous Avez Besoin

- BBC micro:bit V2 (V1 fonctionne mais sans haut-parleur)
- Câble USB ou boîtier à piles
- Navigateur Chrome ou Edge (pour le Web Bluetooth)
- L'application Avions dans le Ciel ouverte

## Démarrage Rapide (2 minutes)

### Étape 1 : Flasher le micro:bit

**Option A — MakeCode (le plus simple, 6 ans et +)**
1. Allez sur [makecode.microbit.org](https://makecode.microbit.org)
2. Nouveau projet → onglet **JavaScript**
3. **Extensions** → cherchez **bluetooth** → ajoutez-le
4. Collez le contenu de `microbit_makecode.js`
5. **Télécharger** → glissez le fichier .hex sur le lecteur micro:bit

**Option B — MicroPython (10 ans et +)**
1. Allez sur [python.microbit.org](https://python.microbit.org)
2. Collez le contenu de `microbit_planes.py`
3. Cliquez **Envoyer au micro:bit**

### Étape 2 : Appairer avec l'application
1. Ouvrez Avions dans le Ciel dans Chrome/Edge
2. Touchez le bouton **🔌** (en haut à droite, à côté de ✏️)
3. Sélectionnez votre micro:bit dans la fenêtre Bluetooth
4. Impulsion verte = connecté !

## Commandes du micro:bit

| Action | Ce Que Ça Fait |
|--------|----------------|
| **Bouton A** | Changer le mode d'affichage : Radar → Compteur → Boussole → Drapeau |
| **Bouton B** | Parcourir les avions, défilement de l'indicatif + distance |
| **Secouer** | Demander des données fraîches à l'application |

## Modes d'Affichage

### 🟢 Radar (par défaut)
La grille LED 5×5 devient un mini écran radar :
- **Point central** = votre position
- **Points autour** = avions à proximité
- Plus brillant = plus haute altitude
- La position correspond au vrai azimut

### 🔢 Compteur
Affiche le nombre total d'avions en grand. Mise à jour toutes les 5 secondes.

### 🧭 Boussole
Une flèche pointe vers l'avion le plus proche. Utilise la boussole + accéléromètre intégrés du micro:bit. Inclinez et tournez pour « trouver » l'avion dans le ciel !

### 🏳️ Drapeau
Affiche le code pays de l'avion le plus proche en défilement sur les LEDs.

## Alertes 🚨

Quand un avion passe à moins de 8 km :
1. Animation d'anneau en expansion sur les LEDs
2. Icône d'avion apparaît
3. Buzzer joue un accord C-E-G ascendant (V2 uniquement)
4. L'indicatif et la distance défilent à l'écran

## Protocole de Données

L'application envoie les données via BLE UART toutes les 5 secondes :

```
U|nombre|cs,dist,azimut,alt,pays|cs,dist,azimut,alt,pays|...
```

Exemple :
```
U|14|AFR123,42.5,210,10668,FR|BAW456,8.1,45,8534,GB|UAE789,95.3,180,11278,AE
```

Messages d'alerte :
```
A|BAW456|5.2|8500|GB
```

Le micro:bit peut répondre :
```
REFRESH
```

## Dépannage

**« Web Bluetooth non supporté »**
→ Utilisez Chrome ou Edge. Safari et Firefox ne supportent pas encore le Web Bluetooth.

**Le micro:bit n'apparaît pas**
→ Vérifiez que Bluetooth est activé dans le code (MakeCode : ajoutez l'extension bluetooth)
→ Redémarrez le micro:bit
→ Dissociez des paramètres Bluetooth du système si déjà apparié

**Pas de données sur les LEDs**
→ Vérifiez l'impulsion verte sur le bouton 🔌
→ Assurez-vous que les avions sont chargés dans l'application
→ Appuyez sur le Bouton A pour être en mode Radar

**La boussole pointe mal**
→ Calibrez : quand le micro:bit affiche « TILT », inclinez-le dans toutes les directions

## Idées de Projets

- 📊 **Enregistreur de données** : ajoutez des appels `datalogger.log()` pour suivre les avions dans le temps
- 🔊 **Notes d'altitude** : associez l'altitude des avions à des notes musicales
- 🌈 **Bandeau NéoPixel** : ajoutez un bandeau LED pour visualiser la densité de trafic
- 📻 **Réseau radio** : plusieurs micro:bits partageant les données par radio
- 🧪 **Projet scientifique** : graphique du nombre d'avions par heure/jour, corrélation avec la météo
