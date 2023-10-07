# 📋 Changelog

All notable changes to Planes in the Sky.

## [1.1.0] — 2026-03-01

### 🌍 Trilingual Release

**Internationalization (i18n)**
- Complete French (Français) translation — 150+ UI strings
- Complete Arabic (العربية) translation — 150+ UI strings with RTL layout
- Language selector in header: EN · FR · AR
- Auto-detection from browser language (navigator.language)
- All dynamic text translated: mode names, shape names, info panel labels, altitude/speed fun facts, atmospheric layers, proximity alerts, onboarding slides, SDR panel, micro:bit status, heritage scholars, expert panels
- Noto Kufi Arabic web font for Arabic UI

**Arabic Virtual Keyboard**
- Full 3-row Arabic letter layout (ض to ظ)
- Tashkeel/diacritics expandable row (fatḥa, ḍamma, kasra, shadda, tanwīn)
- Preview bar with RTL blinking cursor
- Copy, Paste, Select All, Clear buttons
- Smart input targeting (auto-detects focused text field)
- Send/Enter button triggers search or city lookup
- ⌨️ toggle button (bottom-left, visible only in Arabic mode)

**Bismillah & Branding**
- بسم الله الرحمن الرحيم bar at top of viewport (Amiri font, soft gold)
- workshop-diy.org footer link (minimal, low opacity)

**RTL Layout**
- Full right-to-left support: header, info panel, search, heritage panel, SDR panel, loading screen, proximity alerts
- `dir="rtl"` and `lang="ar"` on document root
- CSS scoped under `[dir="rtl"]` selectors

**Trilingual Documentation**
- All docs translated to French and Arabic:
  - README (FR/AR), HELP (FR/AR), FAQ (FR/AR), SDR_GUIDE (FR/AR), MICROBIT_GUIDE (FR/AR)
- Reorganized docs/ into en/, fr/, ar/ subdirectories
- Hardware files moved to hardware/ directory
- New START_HERE.txt quick-start guide

## [1.0.0] — 2026-02-28

### 🎉 First Public Release

**Core App**
- Five progressive modes: Sky, Learn, Pro, Expert, Heritage
- Real-time flight tracking via OpenSky Network API
- Canvas rendering at native DPI with procedural graphics
- Gyroscope/accelerometer parallax with drag fallback
- Automatic day/night/twilight from solar declination algorithm
- 5-slide animated onboarding tutorial
- Country search and filter system
- Demo mode with simulated flights (auto-activates on API failure)
- Loading overlay with animated plane icon

**Nine Aircraft Shapes**
- Airliner (detailed jet with gradient fuselage, engines, windows, nav lights)
- Fighter (delta-wing with canards, twin tails, afterburner glow)
- Prop (straight wings, animated 3-blade propeller)
- Helicopter (spinning main + tail rotors, landing skids)
- Paper Plane (origami fold with crease shadow)
- Rocket (retro style with fins, porthole, flickering exhaust)
- Bird (animated flapping wings, beak, eye)
- UFO (dome, 8 rotating rim lights, tractor beam)
- Star (spinning, pulsing, with sparkle effects)

**Visual Polish**
- Layered clouds with volumetric secondary puffs
- Horizon haze atmospheric gradient
- Moon with craters and glow halo
- Sun with outer halo, bright core, lens flare
- Shooting stars with gradient trails at night
- Segmented fading vapor trails with high-altitude contrail glow
- Navigation lights (red/green/white) at night
- Distance rings at 50/100/150 km
- Enhanced compass with tick marks, cardinal labels, red/white needles
- Coordinate grid overlay in Expert mode

**Interaction**
- Pinch-to-zoom (0.5× to 3×) with double-tap reset
- Animated plane counter with bounce effect
- Proximity alert when a plane is within 8 km
- Haptic feedback on tap and alerts
- Keyboard shortcuts for all major actions
- Sound effects (tap, mode switch, radar ping, wind ambience)

**Data**
- 50 countries with flag, greeting, and 2 fun facts
- 83 airlines recognized by ICAO callsign prefix
- 50+ ICAO hex address ranges for country detection
- 10 cities in location picker
- 9 Islamic Golden Age scholars in Heritage mode

**Hardware Companions**
- micro:bit via Web Bluetooth (LED radar, compass, alerts, buzzer)
  - MakeCode version for ages 6+
  - MicroPython version for ages 10+
- SDR Receiver via RTL-SDR dongle
  - Direct rtl_adsb, dump1090 network, and SBS/BaseStation backends
  - ICAO country detection from hex addresses
  - Live stats (msg/sec, max range, country breakdown)
  - Coverage API for range analysis
  - Raspberry Pi systemd deployment
  - SDR demo mode for UI testing without hardware

**Documentation**
- Comprehensive README with feature overview
- User guide (HELP.md)
- FAQ (FAQ.md)
- SDR setup guide with Raspberry Pi deployment
- micro:bit setup guide
- Interactive documentation page (docs.html)
