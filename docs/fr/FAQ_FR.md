# ❓ Foire Aux Questions

## Général

### Qu'est-ce que c'est ?
Avions dans le Ciel est un traqueur de vols en temps réel qui affiche les avions sur un ciel animé. Conçu pour les enfants et les familles, avec cinq modes progressifs allant du plus simple (4 ans et +) au plus avancé (12 ans et +). C'est un seul fichier HTML — aucune installation nécessaire.

### Comment sait-il où sont les avions ?
Par défaut, il utilise l'API [OpenSky Network](https://opensky-network.org/), qui agrège les données de milliers de récepteurs ADS-B bénévoles dans le monde. Chaque avion commercial émet sa position, son altitude, sa vitesse et son indicatif via des signaux radio ADS-B sur 1090 MHz. En option, vous pouvez recevoir ces signaux vous-même avec un dongle RTL-SDR (voir la section SDR).

### Est-ce gratuit ?
Oui. L'application est gratuite, l'API OpenSky est gratuite (avec des limites de requêtes), et le code source est sous licence MIT.

### Ça fonctionne hors ligne ?
Partiellement. L'application elle-même se charge instantanément sans internet, mais les données de vol en direct nécessitent une connexion réseau. Sans internet, le Mode Démo s'active automatiquement avec des vols simulés.

### Est-ce que ça piste ma position ?
Votre position est utilisée uniquement pour calculer quels avions afficher (~200 km autour) et pour le calcul du lever/coucher de soleil. Les données de localisation sont envoyées à l'API OpenSky sous forme de boîte englobante. Rien n'est stocké ni pisté.

---

## Avions et Données

### Pourquoi je ne vois pas d'avions ?
Plusieurs raisons possibles :
- **Limite de l'API** — OpenSky autorise ~100 requêtes par jour sans compte. Attendez quelques minutes.
- **Zone éloignée** — moins d'avions survolent les zones rurales ou océaniques.
- **Nuit** — certaines régions ont moins de trafic la nuit.
- **Délai d'attente** — l'API peut être temporairement indisponible. L'appli passe en Mode Démo après 2 échecs.

Appuyez sur `D` pour activer le Mode Démo à tout moment.

### Ce sont de vrais avions ?
Oui ! Quand vous êtes connecté à OpenSky (par défaut) ou au SDR, ce sont de vrais avions avec de vraies positions, mises à jour toutes les 10–12 secondes. En Mode Démo (badge doré visible), les avions sont simulés.

### Quelle est la précision de la position ?
Les positions ADS-B sont basées sur le GPS et précises à ~15 mètres. Le délai est de 5 à 15 secondes selon l'API ou le SDR.

### Pourquoi mon avion n'affiche pas de pays ou de compagnie ?
- **Pays** : nécessite l'API OpenSky (qui le fournit) ou la recherche hexadécimale OACI (pour le SDR). Certains avions militaires ou privés n'ont pas d'immatriculation enregistrée.
- **Compagnie** : résolue à partir des 3 premiers caractères de l'indicatif. Certains utilisent des préfixes non standard.

### Que signifient les niveaux de vol ?
Les niveaux de vol (FL) sont des références d'altitude normalisées. FL350 = 35 000 pieds = ~10 668 mètres. Affichés en modes Pro et Expert.

### Qu'est-ce qu'un code SQUAWK ?
Un code transpondeur à 4 chiffres attribué par le contrôle aérien. Codes spéciaux : 7500 (détournement), 7600 (panne radio), 7700 (urgence). Ceux-ci déclenchent des alertes en mode Pro.

---

## Modes

### Par quel mode commencer ?
- **4–5 ans** : Mode Ciel — touchez les avions et voyez les drapeaux
- **6–9 ans** : Mode Découvrir — comparaisons amusantes et faits par pays
- **10–12 ans** : Mode Pro — radar, ambiance de contrôle aérien
- **12 ans et +** : Mode Expert — données aéronautiques réelles
- **Tous âges** : Mode Héritage — histoire de l'Âge d'Or islamique

### Puis-je changer de mode à tout moment ?
Oui. Touchez les pilules de mode en haut ou appuyez sur `1`–`5`. L'avion sélectionné reste sélectionné d'un mode à l'autre.

### Qu'est-ce que le Mode Héritage ?
Il met en lumière les contributions des savants de l'Âge d'Or islamique (VIIIe–XIIIe siècle) aux mathématiques et sciences qui rendent l'aviation moderne possible. Chaque savant est relié aux données de vol en temps réel — par exemple, l'algèbre d'Al-Khwarizmi est montrée calculant la trajectoire réelle d'un avion.

---

## Formes

### Les formes affectent-elles les performances ?
Non. Les 9 formes sont dessinées de manière procédurale sur le canevas avec une complexité similaire. L'avion de ligne (par défaut) est légèrement plus détaillé, mais la différence de performance est négligeable.

### Puis-je avoir des formes différentes par avion ?
Pas actuellement — la forme s'applique à tous les avions. Ce pourrait être une fonctionnalité future.

### Les formes ont-elles des sons ?
Non. Les effets sonores sont liés aux interactions (toucher, changement de mode), pas aux formes.

---

## Audio

### Comment activer le son ?
Touchez le bouton 🔇 (côté droit, sous l'en-tête). Il bascule en 🔊 quand activé.

### Pourquoi pas de son sur mobile ?
Les navigateurs mobiles nécessitent un geste utilisateur avant de jouer de l'audio. Touchez le bouton audio après le chargement. Si ça ne marche toujours pas, vérifiez que votre téléphone n'est pas en mode silencieux.

### Puis-je régler le volume ?
L'appli n'a pas de curseur de volume — utilisez les contrôles de volume de votre appareil. L'ambiance de vent s'adapte automatiquement au nombre d'avions visibles.

---

## Récepteur SDR

### Qu'est-ce que le SDR ?
Radio Définie par Logiciel. Un dongle RTL-SDR (20–30€ sur Amazon) se branche en USB et reçoit les signaux radio, y compris les émissions ADS-B à 1090 MHz des avions.

### Pourquoi utiliser le SDR plutôt que l'API ?
- **Pas besoin d'internet** — idéal pour les sorties scolaires, le camping
- **Mises à jour plus rapides** — temps réel vs. interrogation API toutes les 10 secondes
- **Éducatif** — les enfants apprennent la radio, les signaux et le décodage
- **Pas de limites** — recevez autant d'avions que votre antenne peut capter

### Quel matériel faut-il ?
- Un dongle RTL-SDR Blog V3 ou tout dongle USB basé sur RTL2832U (~25€)
- L'antenne fournie fonctionne, mais une antenne dédiée 1090 MHz améliore la portée
- Un ordinateur (Raspberry Pi, portable ou fixe)

### Quelle est la portée ?
Avec l'antenne de base : 50–150 km. Avec une bonne antenne externe en hauteur : 200–400 km. La ligne de vue est déterminante.

### Puis-je utiliser FlightAware PiAware ?
Oui. Si vous avez déjà un feeder PiAware ou ADS-B Exchange, notre `sdr_receiver.py` peut se connecter à sa sortie dump1090.

---

## micro:bit

### Quelle version de micro:bit ?
BBC micro:bit V2 recommandé (haut-parleur intégré pour les alertes sonores). La V1 fonctionne mais sans son.

### Pourquoi le bouton 🔌 ne fonctionne pas ?
Le bouton est toujours visible. S'il ne fonctionne pas, vérifiez que vous utilisez Chrome ou Edge — le Web Bluetooth n'est pas supporté par Safari ou Firefox.

### Puis-je utiliser micro:bit sans l'appli web ?
Le compagnon micro:bit est conçu pour recevoir des données de l'appli web via Bluetooth. Il ne reçoit pas les signaux ADS-B de manière indépendante.

### Puis-je utiliser micro:bit ET SDR ensemble ?
Absolument ! Le SDR fournit les données, l'appli web les affiche, et le micro:bit vous donne un compagnon physique. Les trois fonctionnent ensemble.

---

## Technique

### Pourquoi un seul fichier HTML ?
La simplicité. Les enseignants peuvent l'envoyer par e-mail, les élèves l'ouvrir depuis une clé USB. Rien à installer ni configurer. Zéro risque de dépendance.

### Ça utilise des cookies ou du stockage local ?
Non. L'application est entièrement sans état. Chaque session démarre à zéro.

### Puis-je l'intégrer dans mon site web ?
Oui. C'est un seul fichier HTML — hébergez-le n'importe où. Vous pouvez utiliser un iframe ou un lien direct.

### Ça fonctionne sur des connexions lentes ?
Le fichier HTML fait ~183 Ko et se charge instantanément. Les appels API font ~5 Ko toutes les 12 secondes. Même en 2G, ça fonctionne.

### Que se passe-t-il sans internet ?
L'appli continue d'afficher les dernières positions connues. Après 2 appels API échoués (~24 secondes), elle passe en Mode Démo. Quand internet revient, appuyez sur `D` pour revenir aux données en direct.

### Puis-je auto-héberger l'API OpenSky ?
Vous pouvez créer un compte OpenSky gratuit pour des limites plus élevées. Pour un usage totalement hors ligne, utilisez le récepteur SDR.

---

## Éducation

### Puis-je l'utiliser en classe ?
Oui ! Quelques idées de cours :
- **Géographie** : filtrer par pays, discuter des routes aériennes, d'où viennent la plupart des avions ?
- **Mathématiques** : calculer vitesse × temps = distance, conversions d'unités
- **Sciences** : couches atmosphériques, température en altitude, formation des traînées
- **Histoire** : le Mode Héritage explore les contributions de l'Âge d'Or islamique
- **Ingénierie** : comment fonctionnent les signaux ADS-B ? (extension SDR)
- **Programmation** : le code est ouvert — les élèves peuvent le lire et le modifier

### Y a-t-il un guide pour les enseignants ?
Pas encore, mais les cinq modes sont conçus comme une progression naturelle. Commencez une séance en Mode Ciel et avancez progressivement.

### Les élèves peuvent-ils modifier le code ?
Oui. C'est un seul fichier HTML avec du JavaScript clairement structuré. Les élèves avancés peuvent ajouter des pays, compagnies, formes, ou des fonctionnalités entièrement nouvelles.

---

## Vie Privée et Sécurité

### Les données sont-elles en temps réel ?
Oui, avec un délai de 5 à 15 secondes. C'est la norme pour les données ADS-B publiques.

### Puis-je suivre un vol spécifique ?
Vous pouvez toucher n'importe quel avion visible pour voir son indicatif, mais l'appli ne permet pas la recherche par numéro de vol. Elle ne montre que les avions actuellement en portée.

### Le trafic militaire est-il affiché ?
Certains avions militaires émettent en ADS-B, beaucoup non. Ceux qui apparaissent s'affichent comme « compagnie inconnue ».

### Y a-t-il des publicités ?
Non. C'est un outil éducatif open source sans publicité, pistage ni monétisation.
