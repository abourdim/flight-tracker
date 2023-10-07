# ✈️ Planes in the Sky — v1.0

**A kid-friendly real-time flight tracker that turns the sky into an interactive classroom.**

Watch real aircraft fly over your head on a beautiful animated sky. Tap any plane to discover its airline, country, altitude, speed — and fun facts. Five progressive modes grow with the learner, from a 4-year-old tapping planes to a 14-year-old reading METAR data. Optional micro:bit companion and SDR receiver for hands-on STEM.

Built as a **single HTML file** — no server, no build tools, no frameworks, no dependencies.

---

## Quick Start

1. Open `index.html` in any modern browser
2. Allow location access (or pick a city)
3. Planes appear in real time. Tap one!

> **No planes?** The app auto-activates Demo Mode with simulated flights after 2 failed API calls. Press `D` to toggle manually.

---

## Five Progressive Modes

| Mode | Ages | What It Shows |
|------|------|---------------|
| 🌤️ **Sky** | 4+ | Beautiful animated sky with parallax, day/night/twilight, layered clouds, moon craters, sun halos. Tap planes to see country flags and greetings. |
| 📚 **Learn** | 6+ | Altitude & speed comparisons ("higher than Mount Everest!"), cultural greetings in native languages, country fun facts with emoji. |
| 📡 **Pro** | 10+ | Full radar display with afterglow sweep, heading arrows, distance readouts, SQUAWK alerts, NOTAM panel. |
| 🔬 **Expert** | 12+ | METAR weather, atmospheric layers, fuel burn estimates, Mach number, contrail prediction, coordinate grid, waypoints, CSV export, sparkline charts. |
| 🕌 **Heritage** | All | Islamic Golden Age scholars timeline — 9 scholars linked to flight math in real time. Al-Khwarizmi's algebra, Ibn al-Haytham's optics, Al-Battani's trigonometry. |

Switch modes with the pills at the top or press `1`–`5`.

---

## Nine Aircraft Shapes

Tap ✏️ or press `S` to cycle through visual styles:

| Shape | Icon | Description |
|-------|------|-------------|
| Airliner | ✈️ | Detailed jet with gradient fuselage, swept wings, twin engines, window dots, nav lights |
| Fighter | 🛩️ | Sleek delta-wing with canards, twin tail fins, cockpit bubble, afterburner glow |
| Prop | 🛫 | Classic propeller plane with straight wings, spinning 3-blade prop (animated) |
| Helicopter | 🚁 | Bulbous body, spinning main + tail rotors, landing skids |
| Paper Plane | 📄 | Origami fold with crease line and subtle shadow |
| Rocket | 🚀 | Retro rocket with nose cone, fins, porthole, flickering dual-color exhaust |
| Bird | 🐦 | Animated flapping wings, tail feathers, beak, eye with pupil |
| UFO | 🛸 | Flying saucer with dome, 8 rotating rim lights, occasional tractor beam |
| Star | ⭐ | Spinning 5-pointed star with radial glow, pulse animation, sparkle |

All shapes respect altitude coloring, night mode, heritage gold tinting, and country filter fade.

---

## Key Features

### Data Sources
- **OpenSky Network API** — default, no setup required
- **SDR Receiver** — live ADS-B from RTL-SDR dongle (see `docs/SDR_GUIDE.md`)
- **Demo Mode** — simulated flights, auto-activates if API is unreachable

### Visual
- Proper **sunrise/sunset** calculated from GPS + solar declination
- **Twilight gradients** — dawn purple → rose → amber → gold
- **Layered clouds** with volumetric secondary puffs
- **Moon** with craters and glow halo / **Sun** with halo and lens flare
- **Horizon haze** atmospheric gradient
- **Distance rings** at 50/100/150km (dashed)
- **Enhanced compass** with cardinal labels, red/white needles, tick marks
- **Shooting stars** at night with gradient trails

### Interaction
- **Country search/filter** — 🔍 or press `F`. Type any country or airline name
- **Pinch-to-zoom** — mobile pinch or mouse wheel, 0.5× to 3×
- **Double-tap/click** resets zoom and pan
- **Proximity alert** — gold notification when a plane is within 8km
- **Animated plane counter** with bounce effect
- **Haptic feedback** on plane tap and proximity alerts
- **Gyroscope parallax** — tilt your phone to look around (with drag fallback)

### Audio
- **Wind ambience** that scales with plane count
- **Tap sound** — descending sine wave on plane selection
- **Mode switch** — ascending triangle wave
- **Radar ping** — entering Pro mode

### Data
- **50 countries** with flag, greeting, and 2 fun facts each
- **83 airlines** recognized by ICAO callsign prefix
- **50+ ICAO hex ranges** for country detection from raw ADS-B
- **10 cities** in the location picker (Paris, London, Dubai, Istanbul, Casablanca, Makkah, New York, Tokyo, Sydney, Singapore)

### Heritage Mode (Islamic Golden Age)
- 9 scholars: Al-Khwarizmi, Abbas ibn Firnas, Ibn al-Haytham, Al-Battani, Al-Biruni, Al-Jazari, Al-Idrisi, Al-Zahrawi, Fatima al-Fihri
- Live connections to flight math (algebra → trajectory, trigonometry → distance, optics → radar)
- Interactive timeline with scholar cards
- Heritage toast notifications linking scholars to real-time data

---

## Hardware Companions

### 🔌 micro:bit (see `docs/MICROBIT_GUIDE.md`)
Connect a BBC micro:bit via Web Bluetooth for a physical control tower:
- LED radar, plane counter, compass pointer, country display
- Overhead alert with expanding ring animation + buzzer
- Two versions: MakeCode (ages 6+) and MicroPython (ages 10+)

### 📡 SDR Receiver (see `docs/SDR_GUIDE.md`)
Receive live ADS-B from aircraft with an RTL-SDR dongle ($25):
- No internet required — data from 1090 MHz radio
- Three backends: rtl_adsb, dump1090, SBS/BaseStation
- Country detection from ICAO hex addresses
- Live stats: messages/sec, max range, country breakdown
- Raspberry Pi deployment with systemd service

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `1`–`5` | Switch modes (Sky, Learn, Pro, Expert, Heritage) |
| `S` | Cycle aircraft shape |
| `F` or `/` | Open country search |
| `D` | Toggle demo mode |
| `+` / `-` | Zoom in / out |
| `R` | Reset zoom & pan |
| `Esc` | Close any open panel / clear filter |

---

## Technical Specs

| Metric | Value |
|--------|-------|
| File | Single `index.html` |
| Size | ~150 KB |
| Lines | ~2,200 |
| Dependencies | None (zero npm, zero CDN) |
| APIs | OpenSky Network, Nominatim (geocoding), Google Fonts |
| Rendering | Canvas 2D at native DPI |
| Audio | Web Audio API (synthesized, no files) |
| Motion | DeviceOrientation API with pointer fallback |
| Bluetooth | Web Bluetooth API (micro:bit) |
| Storage | None (stateless, no cookies) |
| Offline | Works with Demo Mode |

### Browser Support
- ✅ Chrome / Edge 80+ (all features including Web Bluetooth)
- ✅ Safari 14+ (no Web Bluetooth)
- ✅ Firefox 78+ (no Web Bluetooth)
- ✅ Mobile Chrome / Safari
- ✅ PWA-ready (add to home screen)

---

## File Structure

```
planes-in-the-sky-v1.0/
├── index.html              # The app (single file, ~150 KB)
├── README.md               # This file
├── CHANGELOG.md            # Version history
├── LICENSE                  # MIT License
├── sdr_receiver.py         # SDR ADS-B receiver (Python)
├── microbit_planes.py      # micro:bit MicroPython code
├── microbit_makecode.js    # micro:bit MakeCode code
└── docs/
    ├── HELP.md             # User guide
    ├── FAQ.md              # Frequently asked questions
    ├── SDR_GUIDE.md        # SDR setup instructions
    ├── MICROBIT_GUIDE.md   # micro:bit setup instructions
    └── docs.html           # Interactive documentation (open in browser)
```

---

## Credits

- Flight data: [OpenSky Network](https://opensky-network.org/) (free API)
- Geocoding: [Nominatim / OpenStreetMap](https://nominatim.org/)
- ADS-B decoding: [pyModeS](https://github.com/junzis/pyModeS) (SDR mode)
- Islamic Golden Age research: Various academic sources
- Font: Inter (Google Fonts)

---

## License

MIT License — see `LICENSE` file. Free for personal, educational, and commercial use.

---

*Built with love for curious kids who look up at the sky and wonder where those planes are going.* ✈️
