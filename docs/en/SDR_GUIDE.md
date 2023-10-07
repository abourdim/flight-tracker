# 📡 SDR ADS-B Receiver — Setup Guide

## What You Need

### Hardware
- **RTL-SDR dongle** (~$25): RTL-SDR Blog V3, Nooelec NESDR, or any RTL2832U-based USB dongle
- **1090 MHz antenna**: the one included with most RTL-SDR kits works, or build/buy a dedicated ADS-B antenna for better range
- **Computer**: Raspberry Pi, laptop, or desktop (Linux, macOS, or Windows with WSL)

### Software
- Python 3.8+
- RTL-SDR drivers (`rtl-sdr` package)
- Our `sdr_receiver.py` script

## Quick Start

### 1. Install RTL-SDR Drivers

**Linux (Raspberry Pi / Ubuntu / Debian):**
```bash
sudo apt update
sudo apt install rtl-sdr librtlsdr-dev
# Test: plug in dongle, then:
rtl_test -t
```

**macOS:**
```bash
brew install librtlsdr
```

**Windows:**
Use WSL2, or install [Zadig](https://zadig.akeo.ie/) for WinUSB drivers.

### 2. Install Python Dependencies

```bash
pip install pyModeS flask flask-cors
```

### 3. Run the Receiver

```bash
# Basic — auto-detect RTL-SDR dongle
python3 sdr_receiver.py --lat YOUR_LAT --lon YOUR_LON

# Example for Paris
python3 sdr_receiver.py --lat 48.8566 --lon 2.3522

# Custom port
python3 sdr_receiver.py --lat 48.8566 --lon 2.3522 --port 8090
```

### 4. Connect the Web App

1. Open Planes in the Sky in your browser
2. Tap the **📡** button (top-right)
3. Enter `http://localhost:8090` (or your Pi's IP)
4. Tap **Connect**
5. Green pulse = receiving live SDR data!

## Alternative Backends

### Using dump1090

If you already have dump1090 or readsb running:

```bash
# Connect to dump1090's raw output (port 30002)
python3 sdr_receiver.py --dump1090 --lat 48.86 --lon 2.35

# Connect to a remote dump1090
python3 sdr_receiver.py --dump1090 --dump1090-host 192.168.1.50 --lat 48.86 --lon 2.35

# Use SBS/BaseStation format (port 30003)
python3 sdr_receiver.py --sbs --lat 48.86 --lon 2.35
```

### Using FlightAware PiAware

If you have a PiAware setup, it runs dump1090 internally:
```bash
python3 sdr_receiver.py --dump1090 --dump1090-host piaware.local --lat 48.86 --lon 2.35
```

### Using tar1090

tar1090 serves aircraft.json — you could also point the web app at:
`http://piaware.local/tar1090/data/aircraft.json`

## Data Flow

```
RF Signals (1090 MHz)
    ↓
RTL-SDR Dongle (USB)
    ↓
rtl_adsb / dump1090 (demodulation)
    ↓
pyModeS (ADS-B decoding)
    ↓
sdr_receiver.py (tracking + HTTP API)
    ↓ port 8090
Planes in the Sky (web app)
```

## API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /api/aircraft` | Aircraft in OpenSky-compatible format |
| `GET /api/aircraft/raw` | Raw aircraft data with all fields |
| `GET /api/stats` | Receiver statistics (msg/s, range, countries) |
| `GET /api/coverage` | Bearing + distance for coverage plots |
| `GET /health` | Health check |

### Example Response: `/api/stats`
```json
{
  "uptime_seconds": 3600,
  "total_messages": 142857,
  "msg_per_second": 39.7,
  "total_tracked": 89,
  "airborne": 34,
  "max_range_km": 287.4,
  "top_countries": [
    ["France", 12],
    ["Germany", 8],
    ["United Kingdom", 5]
  ]
}
```

## SDR Demo Mode

Don't have an RTL-SDR? Tap **Demo** in the SDR panel to simulate SDR reception with fake ADS-B data. The stats panel, badge, and country breakdown all animate with simulated values.

## Raspberry Pi Setup (Headless)

Perfect for a permanent "listening station":

```bash
# On Raspberry Pi
sudo apt install rtl-sdr python3-pip
pip3 install pyModeS flask flask-cors

# Run on boot (add to /etc/rc.local or create a systemd service)
nohup python3 /home/pi/sdr_receiver.py --lat 48.86 --lon 2.35 --port 8090 &

# Access from any device on your network:
# http://raspberrypi.local:8090
```

### systemd service file (`/etc/systemd/system/planes-sdr.service`):
```ini
[Unit]
Description=Planes in the Sky SDR Receiver
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

## ICAO Country Detection

Raw ADS-B signals don't include a country name, but each aircraft's ICAO hex address encodes its registration country. Our receiver automatically maps:

| Hex Range | Country |
|-----------|---------|
| A00000–AFFFFF | United States |
| C00000–C3FFFF | Canada |
| 400000–43FFFF | France |
| 3C0000–3FFFFF | Germany |
| 840000–87FFFF | United Kingdom |
| 300000–33FFFF | Italy |
| 340000–37FFFF | Spain |
| 780000–7BFFFF | Japan |
| 800000–83FFFF | China |
| 7C0000–7FFFFF | Australia |
| ... | 40+ countries total |

## Range & Performance Tips

- **Antenna placement**: Higher = better. Roof or window mount dramatically improves range.
- **Cable loss**: Keep USB cable short, or use an LNA (low-noise amplifier) near the antenna.
- **Typical range**: 100–250km with basic setup, 300–400km with good antenna.
- **Message rate**: Expect 20–100 messages/second in busy airspace.
- **Filtering**: A 1090 MHz bandpass filter helps if you're near cell towers or broadcast transmitters.

## Troubleshooting

**"rtl_adsb not found"**
→ `sudo apt install rtl-sdr` and make sure the dongle is plugged in

**"usb_open error"**
→ The kernel DVB-T driver has claimed the device. Fix:
```bash
sudo rmmod dvb_usb_rtl28xxu rtl2832 rtl2830
echo 'blacklist dvb_usb_rtl28xxu' | sudo tee /etc/modprobe.d/blacklist-rtl.conf
```

**No aircraft appearing**
→ Check antenna connection. Try `rtl_test -t` to verify the dongle works.
→ Ensure you set `--lat` and `--lon` correctly (needed for position decoding).

**Low message rate**
→ Antenna issue. Move it higher or near a window. Even 1m higher helps.

**Web app says "Cannot reach server"**
→ Check firewall: `sudo ufw allow 8090` or use `--port` with an open port.
→ If accessing from another device, use the machine's IP, not `localhost`.
