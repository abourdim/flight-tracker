# ❓ Frequently Asked Questions

## General

### What is this?
Planes in the Sky is a real-time flight tracker that displays aircraft on an animated sky canvas. It's designed for kids and families, with five progressive modes from simple (ages 4+) to advanced (ages 12+). It's a single HTML file — no installation needed.

### How does it know where planes are?
By default, it uses the [OpenSky Network](https://opensky-network.org/) API, which aggregates data from thousands of volunteer ADS-B receivers worldwide. Every commercial aircraft broadcasts its position, altitude, speed, and callsign via ADS-B radio signals on 1090 MHz. Optionally, you can receive these signals yourself with an RTL-SDR dongle (see SDR section below).

### Is it free?
Yes. The app is free, the OpenSky API is free (with rate limits), and the source code is MIT licensed.

### Does it work offline?
Partially. The app itself loads instantly with no internet, but live plane data requires a network connection. Without internet, Demo Mode activates automatically with simulated flights.

### Does it track my location?
Your location is used only to calculate which planes to show (within ~200 km) and for sunrise/sunset timing. Location data is sent to OpenSky's API as a bounding box. Nothing is stored or tracked.

---

## Planes & Data

### Why don't I see any planes?
Several possible reasons:
- **API rate limit** — OpenSky allows ~100 requests per day without an account. Wait a few minutes.
- **Remote location** — fewer planes fly over rural or ocean areas.
- **Night** — some regions have less traffic overnight.
- **Timeout** — the API occasionally goes down. The app auto-switches to Demo Mode after 2 failures.

Press `D` to toggle Demo Mode for simulated flights anytime.

### Are these real planes?
Yes! When connected to OpenSky (default) or SDR, these are real aircraft with real positions, updated every 10–12 seconds. In Demo Mode (indicated by the gold badge), planes are simulated.

### How accurate is the position?
ADS-B positions are GPS-based and accurate to ~15 meters. The delay is 5–15 seconds depending on the API or SDR update rate.

### Why doesn't my plane show a country or airline?
- **Country**: requires either the OpenSky API (which provides it) or ICAO hex lookup (for SDR). Some military or private aircraft don't have mapped registrations.
- **Airline**: resolved from the first 3 characters of the callsign (ICAO airline designator). Some callsigns use non-standard prefixes.

### What do the flight levels mean?
Flight levels (FL) are standardized altitude references. FL350 = 35,000 feet = ~10,668 meters. They're shown in Pro and Expert modes.

### What's a SQUAWK code?
A 4-digit transponder code assigned by air traffic control. Special codes: 7500 (hijack), 7600 (radio failure), 7700 (emergency). These trigger alerts in Pro mode.

---

## Modes

### Which mode should I start with?
- **Ages 4–5**: Sky Mode — just tap planes and see flags
- **Ages 6–9**: Learn Mode — fun comparisons and country facts
- **Ages 10–12**: Pro Mode — radar display, feels like air traffic control
- **Ages 12+**: Expert Mode — real aviation data
- **Any age**: Heritage Mode — Islamic Golden Age history

### Can I switch modes anytime?
Yes. Tap the mode pills at the top or press `1`–`5`. Your selected plane stays selected across mode switches.

### What's Heritage Mode about?
It highlights the contributions of Islamic Golden Age scholars (8th–13th century) to the mathematics and science that make modern aviation possible. Each scholar is connected to real-time flight data — for example, Al-Khwarizmi's algebra is shown computing the actual trajectory of a plane overhead.

---

## Shapes

### Do shapes affect performance?
No. All 9 shapes are drawn procedurally on the canvas with similar complexity. The jet (default) is slightly more detailed with window dots and engine nacelles, but the performance difference is negligible.

### Can I set different shapes for different planes?
Not currently — the shape applies globally to all planes. This could be a future feature.

### Do shapes have sounds?
No. Sound effects are tied to interactions (tap, mode switch), not shapes.

---

## Audio

### How do I enable sound?
Tap the 🔇 button (right side, below the header). It toggles to 🔊 when enabled.

### Why is there no sound on mobile?
Mobile browsers require a user gesture before playing audio. Tap the audio button after the page loads. If it still doesn't work, check that your phone isn't in silent mode.

### Can I adjust the volume?
The app doesn't have a volume slider — use your device's volume controls. The wind ambience auto-scales based on how many planes are visible.

---

## SDR Receiver

### What's SDR?
Software-Defined Radio. An RTL-SDR dongle ($20–$30 on Amazon) plugs into USB and receives radio signals, including the 1090 MHz ADS-B broadcasts from aircraft.

### Why use SDR instead of the API?
- **No internet needed** — great for remote locations, field trips, camping
- **Faster updates** — real-time vs. 10-second API polling
- **Educational** — kids learn about radio, signals, and decoding
- **No rate limits** — receive as many planes as you can hear

### What hardware do I need?
- RTL-SDR Blog V3 or any RTL2832U-based USB dongle (~$25)
- The included antenna works, but a dedicated 1090 MHz antenna improves range (100→300+ km)
- A computer (Raspberry Pi, laptop, or desktop)

### How far can I receive?
With the basic included antenna: 50–150 km. With a good external antenna placed high: 200–400 km. Line of sight matters — higher antenna = better range.

### Can I use FlightAware PiAware?
Yes. If you already have a PiAware or ADS-B Exchange feeder, our `sdr_receiver.py` can connect to its dump1090 output.

---

## micro:bit

### Which micro:bit do I need?
BBC micro:bit V2 is recommended (has a built-in speaker for buzzer alerts). V1 works but without sound.

### Why doesn't the 🔌 button appear?
The button is always visible. If it doesn't work, make sure you're using Chrome or Edge — Web Bluetooth isn't supported in Safari or Firefox.

### Can I use micro:bit without the web app?
The micro:bit companion is designed to receive data from the web app via Bluetooth. It doesn't independently receive ADS-B signals (you'd need an SDR for that).

### Can I use both micro:bit and SDR?
Absolutely! The SDR provides the data, the web app displays it, and the micro:bit gives you a physical companion. All three work together.

---

## Technical

### Why a single HTML file?
Simplicity. Teachers can email it, students can open it from a USB stick, there's nothing to install or configure. It also means zero supply-chain risk and easy archival.

### Does it use cookies or local storage?
No. The app is completely stateless. Every session starts fresh.

### Can I embed it in my website?
Yes. It's a single HTML file — host it anywhere. You can use an iframe or link directly.

### Does it work on slow connections?
The HTML file is ~150 KB and loads instantly. API calls are ~5 KB every 12 seconds. Even on 2G, it works fine (just with slightly delayed plane positions).

### What happens when I lose internet?
The app keeps showing the last known positions. After 2 failed API calls (~24 seconds), it auto-switches to Demo Mode. When internet returns, press `D` to re-enable live data.

### Can I self-host the OpenSky API?
You can register for a free OpenSky account for higher rate limits. For fully offline use, use the SDR receiver.

---

## Education

### Can I use this in my classroom?
Yes! Here are some lesson ideas:
- **Geography**: Filter by country, discuss trade routes, where do most planes come from?
- **Math**: Calculate speed × time = distance, convert units (km→miles, m→ft)
- **Science**: Atmospheric layers, temperature at altitude, contrail formation
- **History**: Heritage Mode explores Islamic Golden Age contributions to flight math
- **Engineering**: How do ADS-B signals work? (SDR extension)
- **Coding**: The app is open source — students can read and modify it

### Is there a teacher's guide?
Not yet, but the five modes are designed as a natural progression. Start a class on Sky Mode and advance through the session.

### Can students modify the code?
Yes. It's a single HTML file with clearly structured JavaScript. Advanced students can add countries, airlines, shapes, or entirely new features.

---

## Privacy & Safety

### Is the data real-time?
Yes, with a 5–15 second delay. This is standard for public ADS-B data.

### Can I track a specific flight?
You can tap any visible plane to see its callsign, but the app doesn't support flight number lookup. It only shows planes currently in range.

### Is military traffic shown?
Some military aircraft broadcast ADS-B; many don't. Military flights that do appear will show as "Unknown" airline.

### Are there ads?
No. This is an open-source educational tool with no ads, tracking, or monetization.
