# 📡 Récepteur SDR ADS-B — Guide d'Installation

## Ce Dont Vous Avez Besoin

### Matériel
- **Dongle RTL-SDR** (~25€) : RTL-SDR Blog V3, Nooelec NESDR, ou tout dongle USB basé sur RTL2832U
- **Antenne 1090 MHz** : celle fournie avec la plupart des kits RTL-SDR fonctionne, ou achetez/construisez une antenne ADS-B dédiée pour plus de portée
- **Ordinateur** : Raspberry Pi, ordinateur portable ou fixe (Linux, macOS, ou Windows avec WSL)

### Logiciel
- Python 3.8+
- Pilotes RTL-SDR (paquet `rtl-sdr`)
- Notre script `sdr_receiver.py`

## Démarrage Rapide

### 1. Installer les Pilotes RTL-SDR

**Linux (Raspberry Pi / Ubuntu / Debian) :**
```bash
sudo apt update
sudo apt install rtl-sdr librtlsdr-dev
# Test : branchez le dongle, puis :
rtl_test -t
```

**macOS :**
```bash
brew install librtlsdr
```

**Windows :**
Utilisez WSL2, ou installez [Zadig](https://zadig.akeo.ie/) pour les pilotes WinUSB.

### 2. Installer les Dépendances Python

```bash
pip install pyModeS flask flask-cors
```

### 3. Lancer le Récepteur

```bash
# Basique — détection auto du dongle RTL-SDR
python3 sdr_receiver.py --lat VOTRE_LAT --lon VOTRE_LON

# Exemple pour Paris
python3 sdr_receiver.py --lat 48.8566 --lon 2.3522

# Port personnalisé
python3 sdr_receiver.py --lat 48.8566 --lon 2.3522 --port 8090
```

### 4. Connecter l'Application Web

1. Ouvrez Avions dans le Ciel dans votre navigateur
2. Touchez le bouton **📡** (en haut à droite)
3. Entrez `http://localhost:8090` (ou l'IP de votre Pi)
4. Touchez **Connecter**
5. Impulsion verte = données SDR en direct reçues !

## Backends Alternatifs

### Utiliser dump1090

Si vous avez déjà dump1090 ou readsb en fonctionnement :

```bash
# Connecter à la sortie brute de dump1090 (port 30002)
python3 sdr_receiver.py --dump1090 --lat 48.86 --lon 2.35

# Connecter à un dump1090 distant
python3 sdr_receiver.py --dump1090 --dump1090-host 192.168.1.50 --lat 48.86 --lon 2.35

# Utiliser le format SBS/BaseStation (port 30003)
python3 sdr_receiver.py --sbs --lat 48.86 --lon 2.35
```

### Utiliser FlightAware PiAware

Si vous avez un PiAware, il exécute dump1090 en interne :
```bash
python3 sdr_receiver.py --dump1090 --dump1090-host piaware.local --lat 48.86 --lon 2.35
```

## Flux de Données

```
Signaux RF (1090 MHz)
    ↓
Dongle RTL-SDR (USB)
    ↓
rtl_adsb / dump1090 (démodulation)
    ↓
pyModeS (décodage ADS-B)
    ↓
sdr_receiver.py (suivi + API HTTP)
    ↓ port 8090
Avions dans le Ciel (appli web)
```

## Points d'Accès API

| Point d'accès | Description |
|----------------|-------------|
| `GET /api/aircraft` | Avions au format compatible OpenSky |
| `GET /api/aircraft/raw` | Données brutes avec tous les champs |
| `GET /api/stats` | Statistiques du récepteur (msg/s, portée, pays) |
| `GET /api/coverage` | Azimut + distance pour les graphiques de couverture |
| `GET /health` | Vérification de santé |

## Mode Démo SDR

Pas de dongle RTL-SDR ? Touchez **Démo** dans le panneau SDR pour simuler la réception SDR avec de fausses données ADS-B. Les statistiques, le badge et la ventilation par pays s'animent avec des valeurs simulées.

## Installation Raspberry Pi (Sans Écran)

Parfait pour une « station d'écoute » permanente :

```bash
# Sur Raspberry Pi
sudo apt install rtl-sdr python3-pip
pip3 install pyModeS flask flask-cors

# Lancer au démarrage (ajoutez à /etc/rc.local ou créez un service systemd)
nohup python3 /home/pi/sdr_receiver.py --lat 48.86 --lon 2.35 --port 8090 &

# Accès depuis tout appareil sur votre réseau :
# http://raspberrypi.local:8090
```

### Fichier service systemd (`/etc/systemd/system/planes-sdr.service`) :
```ini
[Unit]
Description=Récepteur SDR Avions dans le Ciel
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/pi/sdr_receiver.py --lat 48.86 --lon 2.35
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable planes-sdr
sudo systemctl start planes-sdr
```

## Détection de Pays par ICAO

Les signaux ADS-B bruts ne contiennent pas le nom du pays, mais l'adresse hexadécimale ICAO de chaque avion encode son pays d'immatriculation. Notre récepteur fait le mappage automatiquement :

| Plage Hex | Pays |
|-----------|------|
| A00000–AFFFFF | États-Unis |
| C00000–C3FFFF | Canada |
| 400000–43FFFF | France |
| 3C0000–3FFFFF | Allemagne |
| 840000–87FFFF | Royaume-Uni |
| 300000–33FFFF | Italie |
| 340000–37FFFF | Espagne |
| 780000–7BFFFF | Japon |
| 800000–83FFFF | Chine |
| 7C0000–7FFFFF | Australie |
| ... | 40+ pays au total |

## Conseils de Portée et Performance

- **Placement de l'antenne** : plus haut = mieux. Un montage sur toit ou fenêtre améliore considérablement la portée.
- **Perte de câble** : gardez le câble USB court, ou utilisez un LNA (amplificateur faible bruit) près de l'antenne.
- **Portée typique** : 100–250 km en installation de base, 300–400 km avec bonne antenne.
- **Débit de messages** : attendez 20–100 messages/seconde dans un espace aérien fréquenté.
- **Filtrage** : un filtre passe-bande 1090 MHz aide si vous êtes près d'antennes relais.

## Dépannage

**« rtl_adsb introuvable »**
→ `sudo apt install rtl-sdr` et vérifiez que le dongle est branché

**« usb_open error »**
→ Le pilote noyau DVB-T a réclamé l'appareil :
```bash
sudo rmmod dvb_usb_rtl28xxu rtl2832 rtl2830
echo 'blacklist dvb_usb_rtl28xxu' | sudo tee /etc/modprobe.d/blacklist-rtl.conf
```

**Aucun avion n'apparaît**
→ Vérifiez la connexion de l'antenne. Essayez `rtl_test -t` pour vérifier le dongle.
→ Vérifiez que `--lat` et `--lon` sont corrects (nécessaires pour le décodage de position).

**Faible débit de messages**
→ Problème d'antenne. Déplacez-la plus haut ou près d'une fenêtre.

**L'appli indique « Impossible d'atteindre le serveur »**
→ Vérifiez le pare-feu : `sudo ufw allow 8090`
→ Depuis un autre appareil, utilisez l'IP de la machine, pas `localhost`.
