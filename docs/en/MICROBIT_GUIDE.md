# 🔌 micro:bit Companion — Setup Guide

## What You Need

- BBC micro:bit V2 (V1 works but no speaker)
- USB cable or battery pack
- Chrome or Edge browser (for Web Bluetooth)
- The Planes in the Sky web app running

## Quick Start (2 minutes)

### Step 1: Flash the micro:bit

**Option A — MakeCode (easiest, ages 6+)**
1. Go to [makecode.microbit.org](https://makecode.microbit.org)
2. Create new project → click **JavaScript** tab
3. Click **Extensions** → search **bluetooth** → add it
4. Paste the contents of `microbit_makecode.js`
5. Click **Download** → drag .hex file to your micro:bit drive

**Option B — MicroPython (ages 10+)**
1. Go to [python.microbit.org](https://python.microbit.org)
2. Paste the contents of `microbit_planes.py`
3. Click **Send to micro:bit**

### Step 2: Pair with the web app
1. Open Planes in the Sky in Chrome/Edge
2. Tap the **🔌** button (top-right, next to ✏️)
3. Select your micro:bit from the Bluetooth popup
4. Green pulse = connected!

## micro:bit Controls

| Action | What It Does |
|--------|-------------|
| **Button A** | Cycle display mode: Radar → Count → Compass → Flag |
| **Button B** | Cycle through planes, scroll callsign + distance |
| **Shake** | Request fresh data from the web app |

## Display Modes

### 🟢 Radar (default)
The 5×5 LED grid becomes a tiny radar screen:
- **Center dot** = your location
- **Surrounding dots** = planes nearby
- Brighter = higher altitude
- Position matches real compass bearing

### 🔢 Count
Shows the total number of planes as a big number. Updates every 5 seconds.

### 🧭 Compass
An arrow points toward the nearest plane. Uses the micro:bit's built-in compass + accelerometer. Tilt and rotate your micro:bit to "find" the plane in the sky!

### 🏳️ Flag
Shows the country code of the nearest plane scrolling across the LEDs.

## Alerts 🚨

When a plane passes within 8km:
1. Expanding ring animation plays on LEDs
2. Plane icon appears
3. Buzzer plays ascending C-E-G chord (V2 only)
4. Callsign and distance scroll across screen

## Data Protocol

The web app sends data over BLE UART every 5 seconds:

```
U|count|cs,dist,bearing,alt,country|cs,dist,bearing,alt,country|...
```

Example:
```
U|14|AFR123,42.5,210,10668,FR|BAW456,8.1,45,8534,GB|UAE789,95.3,180,11278,AE
```

Alert messages:
```
A|BAW456|5.2|8500|GB
```

micro:bit can send back:
```
REFRESH
```

## Troubleshooting

**"Web Bluetooth not supported"**
→ Use Chrome or Edge. Safari and Firefox don't support Web Bluetooth yet.

**micro:bit not showing up**
→ Make sure Bluetooth is enabled in the micro:bit code (MakeCode: add bluetooth extension)
→ Power cycle the micro:bit
→ Unpair from system Bluetooth settings if previously paired

**No data appearing on LEDs**
→ Check the green pulse on the 🔌 button — it should be glowing
→ Make sure planes are loaded in the web app first
→ Press Button A to make sure you're in Radar mode

**Compass mode points wrong way**
→ Calibrate: when micro:bit shows "TILT", tilt it in all directions until the screen fills

## Project Ideas

- 📊 **Data Logger**: Add `datalogger.log()` calls to track planes over time
- 🔊 **Altitude Tones**: Map plane altitude to musical notes
- 🌈 **NeoPixel Strip**: Add a strip for traffic density visualization
- 📻 **Radio Network**: Multiple micro:bits sharing plane data via radio
- 🧪 **Science Fair**: Graph plane count by hour/day, correlate with weather
