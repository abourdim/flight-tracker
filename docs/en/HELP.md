# 📖 Planes in the Sky — User Guide

## Getting Started

### Opening the App
Open `index.html` in Chrome, Edge, Safari, or Firefox. No installation needed.

### Choosing Your Location
On first launch, you'll see the location picker:

- **📍 Use My Location** — uses your device's GPS (most accurate, recommended)
- **City buttons** — tap any of the 10 preset cities: Paris, London, Dubai, Istanbul, Casablanca, Makkah, New York, Tokyo, Sydney, Singapore
- **Search** — type any city name and tap the result (uses Nominatim geocoding)

Your location determines which planes appear. The app tracks flights within ~200 km of your position.

### First-Time Tutorial
A 5-slide walkthrough appears after choosing your location:
1. Welcome introduction
2. How to tap planes
3. Country search feature
4. The five modes explained
5. Ready to go!

Tap **Skip** or swipe through. The tutorial only appears once.

---

## The Sky View

### What You See
- **Animated sky** — gradient background changes based on time of day at your location
- **Stars** — twinkle at night with random phases, shooting stars streak across occasionally
- **Sun / Moon** — positioned in the sky. Sun has a warm halo and subtle lens flare. Moon has visible craters and a glow
- **Clouds** — layered for depth, drift slowly across the sky
- **Planes** — positioned by real GPS coordinates. Size reflects altitude (higher = smaller). Colors shift by altitude
- **Vapor trails** — segmented fading trails behind each plane, with high-altitude contrail glow
- **Distance rings** — dashed circles at 50, 100, and 150 km from you
- **Compass** — bottom-right corner, shows cardinal directions with red north needle

### Day, Night & Twilight
The sky automatically calculates sunrise and sunset using your GPS coordinates and solar declination:
- **Day** — blue sky gradient
- **Twilight** — golden hour with purple → rose → amber → gold gradients (~36 min around sunrise/sunset)
- **Night** — deep blue to space black, stars visible, moon with craters

### Parallax
Tilt your phone (or drag on desktop) to look around the sky. Stars, clouds, and the sun/moon shift at different depths for a 3D effect.

---

## Interacting with Planes

### Tapping a Plane
Tap/click any plane to open the info panel. You'll see:

- **Callsign** — the flight's radio identifier (e.g., "AFR1234")
- **Airline** — resolved from the callsign prefix (e.g., "Air France")
- **Altitude** — in meters, with fun comparison ("higher than Mount Everest!")
- **Speed** — in km/h, with fun comparison ("faster than a cheetah!")
- **Mach number** — corrected for temperature at altitude
- **Heading** — compass direction with label (N, NE, E, etc.)
- **Vertical speed** — climbing, descending, or cruising
- **Temperature** — estimated at that altitude
- **Country** — flag emoji, native greeting, and 2 fun facts
- **Distance** — how far the plane is from you in km

### Selection Glow
The selected plane gets a pulsing golden glow ring so you can track it visually.

### Closing the Panel
Tap the ✕ button, tap outside the panel, or press `Esc`.

---

## Modes

### 🌤️ Sky Mode (Ages 4+)
Pure visual experience. Beautiful sky, animated planes, minimal text. Perfect for young children. Tap a plane to see its country flag and greeting.

### 📚 Learn Mode (Ages 6+)
Everything in Sky Mode plus:
- Callsign labels appear next to each plane
- Fun altitude and speed comparisons in the info panel
- Country greetings in the native language ("Bonjour!", "مرحبا!", "こんにちは!")
- Two fun facts per country with emoji

### 📡 Pro Mode (Ages 10+)
Full radar display replaces the sky:
- Dark green-on-black CRT aesthetic
- Rotating sweep line with 12-segment afterglow trail
- Four range rings (50, 100, 150, 200 km) with labels
- Crosshairs and N/S/E/W cardinal labels
- Each plane blip shows: callsign, flight level, and distance
- Heading arrows show which direction each plane is flying
- Blips pulse brighter as the sweep line passes them
- SQUAWK panel shows special transponder codes
- NOTAM alert panel

### 🔬 Expert Mode (Ages 12+)
Everything visible on the sky canvas plus:
- Purple coordinate grid overlay
- Distance rings visible with purple styling
- **Info panel extras**: estimated fuel burn (kg/hr), contrail likelihood, atmospheric layer (troposphere/stratosphere/etc.), distance from you, ISS altitude percentage, bearing
- Sparkline altitude charts
- METAR-like weather data
- Waypoint system
- Heatmap visualization
- CSV data export

### 🕌 Heritage Mode (All Ages)
The sky turns golden. A scrollable timeline of 9 Islamic Golden Age scholars appears:
- **Al-Khwarizmi** (780–850) — algebra and algorithms
- **Abbas ibn Firnas** (810–887) — first human flight attempt
- **Ibn al-Haytham** (965–1040) — optics and the scientific method
- **Al-Battani** (858–929) — spherical trigonometry
- **Al-Biruni** (973–1048) — Earth's circumference calculation
- **Al-Jazari** (1136–1206) — mechanical engineering
- **Al-Idrisi** (1100–1165) — world cartography
- **Al-Zahrawi** (936–1013) — surgical instruments
- **Fatima al-Fihri** (800–880) — founded the world's first university

When you tap a plane in Heritage Mode, the info panel shows live connections: "Al-Khwarizmi's algorithms compute this trajectory" with the real heading and speed values.

---

## Country Search & Filter

### Opening Search
Tap 🔍 in the top-right or press `F` or `/`.

### Filtering
Type a country name (e.g., "France") or airline name (e.g., "Air France"). The app:
- Shows matching countries with flags and plane counts
- Highlights matching planes with a golden glow
- Fades non-matching planes to near-transparent
- Shows a flag badge next to matching planes

### Clearing
Tap the ✕ in the search bar, press `Esc`, or tap "Clear Filter".

### Available Countries
The search shows all countries currently represented in the sky, sorted by plane count. Matching uses both the aircraft's registration country and its airline's home country.

---

## Aircraft Shapes

### Changing Shape
- Tap ✏️ (pencil button, top-right) to open the shape picker grid
- Press `S` to cycle through shapes sequentially
- Shape applies to all planes on screen

### Shape Details
Each shape is procedurally rendered on the canvas with:
- Altitude-based color gradients (higher = lighter)
- Night mode color adjustments
- Heritage mode gold tinting
- Country filter opacity
- Unique animations where applicable (propeller spin, wing flap, rocket flame, UFO wobble)

Navigation lights (red port, green starboard, white tail strobe) appear at night on jet, fighter, and prop shapes.

---

## Zoom & Pan

### Zooming
- **Mobile**: pinch gesture (0.5× to 3×)
- **Desktop**: mouse scroll wheel
- **Keyboard**: `+` to zoom in, `-` to zoom out

### Panning
- **Mobile**: tilt phone (gyroscope) or one-finger drag
- **Desktop**: click and drag

### Resetting
- **Mobile**: double-tap
- **Desktop**: double-click
- **Keyboard**: `R`

The zoom level appears briefly as a floating pill (e.g., "1.5×") in the bottom-right.

---

## Audio

Toggle audio with the 🔇/🔊 button (below the header, right side).

When enabled:
- **Wind ambience** — continuous low background that scales with plane density
- **Tap sound** — short descending tone when you tap a plane
- **Mode switch** — ascending tone when changing modes
- **Radar ping** — longer sweep tone when entering Pro mode

All sounds are synthesized via Web Audio API — no audio files needed.

---

## Proximity Alerts

When any tracked plane passes within **8 km** of your position:
- A gold notification bar slides down from the top
- Shows: airline name, altitude, and distance
- Subtle haptic vibration on supported devices
- Auto-dismisses after 5 seconds
- 30-second cooldown between alerts

---

## Demo Mode

### What It Is
Simulated flights around your location with realistic data: random callsigns, altitudes, headings, speeds, and countries.

### When It Activates
- Automatically after 2 consecutive API failures (e.g., no internet, OpenSky rate limit)
- A gold "✈️ DEMO MODE — simulated flights" badge appears at the bottom

### Manual Toggle
Press `D` to toggle demo mode on/off. Tap the demo badge to deactivate.

---

## SDR Receiver

### What It Is
Instead of internet data, receive ADS-B signals directly from aircraft overhead using a $25 RTL-SDR USB dongle.

### Connecting
1. Run `sdr_receiver.py` on a computer with the dongle
2. In the app, tap 📡 (top-right)
3. Enter the server URL (default: `http://localhost:8090`)
4. Tap **Connect**

### SDR Demo
Tap **Demo** in the SDR panel to simulate SDR reception without hardware. Stats panel animates with fake message rates and country breakdowns.

### Details
See `docs/SDR_GUIDE.md` for full setup including Raspberry Pi deployment.

---

## micro:bit Companion

### What It Is
A BBC micro:bit becomes a physical "control tower" — LED radar, plane counter, compass pointer, and overhead buzzer alerts.

### Connecting
1. Flash the micro:bit with `microbit_makecode.js` or `microbit_planes.py`
2. In the app, tap 🔌 (top-right)
3. Select your micro:bit from the Bluetooth popup (Chrome/Edge only)

### Details
See `docs/MICROBIT_GUIDE.md` for full setup and button controls.

---

## Troubleshooting Quick Reference

| Problem | Solution |
|---------|----------|
| No planes appear | Wait 10 seconds, or press `D` for demo mode |
| "Location denied" | Pick a city from the picker instead |
| Planes appear then vanish | OpenSky API rate limit — wait 10 seconds |
| Sky is black | You're in night mode! It's night at your location |
| Shapes don't change | Tap ✏️ or press `S` |
| No sound | Tap the 🔇 button to enable audio |
| micro:bit won't connect | Use Chrome or Edge (Web Bluetooth required) |
| SDR shows "cannot reach" | Check that `sdr_receiver.py` is running |

For more troubleshooting, see `docs/FAQ.md`.
