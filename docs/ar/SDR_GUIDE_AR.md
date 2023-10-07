# 📡 مستقبل SDR ADS-B — دليل الإعداد

## ما تحتاجه

### العتاد
- **دونغل RTL-SDR** (~25$): RTL-SDR Blog V3 أو Nooelec NESDR أو أي دونغل USB مبني على RTL2832U
- **هوائي 1090 MHz**: المرفق مع معظم أطقم RTL-SDR يعمل، أو اشترِ/اصنع هوائي ADS-B مخصصاً لمدى أفضل
- **حاسوب**: Raspberry Pi أو محمول أو مكتبي (Linux أو macOS أو Windows مع WSL)

### البرمجيات
- Python 3.8+
- تعريفات RTL-SDR (حزمة `rtl-sdr`)
- سكريبت `sdr_receiver.py` الخاص بنا

## البدء السريع

### 1. تثبيت تعريفات RTL-SDR

**Linux (Raspberry Pi / Ubuntu / Debian):**
```bash
sudo apt update
sudo apt install rtl-sdr librtlsdr-dev
# اختبار: أوصل الدونغل ثم:
rtl_test -t
```

**macOS:**
```bash
brew install librtlsdr
```

**Windows:**
استخدم WSL2، أو ثبّت [Zadig](https://zadig.akeo.ie/) لتعريفات WinUSB.

### 2. تثبيت تبعيات Python

```bash
pip install pyModeS flask flask-cors
```

### 3. تشغيل المستقبل

```bash
# أساسي — كشف تلقائي لدونغل RTL-SDR
python3 sdr_receiver.py --lat خط_العرض --lon خط_الطول

# مثال لباريس
python3 sdr_receiver.py --lat 48.8566 --lon 2.3522

# مثال لدبي
python3 sdr_receiver.py --lat 25.2048 --lon 55.2708

# منفذ مخصص
python3 sdr_receiver.py --lat 25.2048 --lon 55.2708 --port 8090
```

### 4. توصيل التطبيق

1. افتح طائرات في السماء في المتصفح
2. اضغط زر **📡** (أعلى اليمين)
3. أدخل `http://localhost:8090` (أو IP الراسبيري باي)
4. اضغط **اتصال**
5. نبضة خضراء = بيانات SDR مباشرة تُستقبل!

## أنظمة خلفية بديلة

### استخدام dump1090

إذا كان dump1090 أو readsb يعمل لديك:

```bash
# الاتصال بمخرج dump1090 الخام (المنفذ 30002)
python3 sdr_receiver.py --dump1090 --lat 48.86 --lon 2.35

# الاتصال بـ dump1090 بعيد
python3 sdr_receiver.py --dump1090 --dump1090-host 192.168.1.50 --lat 48.86 --lon 2.35

# استخدام صيغة SBS/BaseStation (المنفذ 30003)
python3 sdr_receiver.py --sbs --lat 48.86 --lon 2.35
```

### استخدام FlightAware PiAware

إذا كان لديك PiAware، يُشغّل dump1090 داخلياً:
```bash
python3 sdr_receiver.py --dump1090 --dump1090-host piaware.local --lat 48.86 --lon 2.35
```

## تدفّق البيانات

```
إشارات RF (1090 MHz)
    ↓
دونغل RTL-SDR (USB)
    ↓
rtl_adsb / dump1090 (فك التعديل)
    ↓
pyModeS (فك تشفير ADS-B)
    ↓
sdr_receiver.py (التتبع + واجهة HTTP)
    ↓ المنفذ 8090
طائرات في السماء (التطبيق)
```

## نقاط الوصول API

| النقطة | الوصف |
|--------|-------|
| `GET /api/aircraft` | الطائرات بصيغة متوافقة مع OpenSky |
| `GET /api/aircraft/raw` | بيانات خام بكل الحقول |
| `GET /api/stats` | إحصائيات المستقبل (رسالة/ث، المدى، البلدان) |
| `GET /api/coverage` | السمت + المسافة لرسم التغطية |
| `GET /health` | فحص الحالة |

## الوضع التجريبي SDR

ليس لديك دونغل RTL-SDR؟ اضغط **تجريبي** في لوحة SDR لمحاكاة الاستقبال ببيانات ADS-B وهمية. الإحصائيات والشارة وتوزيع البلدان كلها تتحرك بقيم محاكاة.

## إعداد Raspberry Pi (بدون شاشة)

مثالي لـ «محطة استماع» دائمة:

```bash
# على Raspberry Pi
sudo apt install rtl-sdr python3-pip
pip3 install pyModeS flask flask-cors

# التشغيل عند الإقلاع
nohup python3 /home/pi/sdr_receiver.py --lat 25.20 --lon 55.27 --port 8090 &

# الوصول من أي جهاز على شبكتك:
# http://raspberrypi.local:8090
```

### ملف خدمة systemd (`/etc/systemd/system/planes-sdr.service`):
```ini
[Unit]
Description=مستقبل SDR طائرات في السماء
After=network.target

[Service]
ExecStart=/usr/bin/python3 /home/pi/sdr_receiver.py --lat 25.20 --lon 55.27
Restart=always
User=pi

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable planes-sdr
sudo systemctl start planes-sdr
```

## كشف البلد عبر ICAO

إشارات ADS-B الخام لا تحتوي اسم البلد، لكن العنوان الست عشري ICAO لكل طائرة يشفّر بلد تسجيلها. مستقبلنا يربطها تلقائياً:

| النطاق الست عشري | البلد |
|------------------|-------|
| A00000–AFFFFF | الولايات المتحدة |
| C00000–C3FFFF | كندا |
| 400000–43FFFF | فرنسا |
| 3C0000–3FFFFF | ألمانيا |
| 840000–87FFFF | المملكة المتحدة |
| 300000–33FFFF | إيطاليا |
| 340000–37FFFF | إسبانيا |
| 780000–7BFFFF | اليابان |
| 800000–83FFFF | الصين |
| 7C0000–7FFFFF | أستراليا |
| ... | +40 دولة إجمالاً |

## نصائح المدى والأداء

- **وضع الهوائي**: أعلى = أفضل. التركيب على السطح أو النافذة يحسّن المدى بشكل كبير.
- **فقد الكابل**: أبقِ كابل USB قصيراً، أو استخدم مُضخّم منخفض الضجيج (LNA) قرب الهوائي.
- **المدى النموذجي**: 100–250 كم بالإعداد الأساسي، 300–400 كم بهوائي جيد.
- **معدل الرسائل**: توقع 20–100 رسالة/ثانية في مجال جوي مزدحم.
- **الفلترة**: مرشح تمرير نطاقي 1090 MHz يساعد إذا كنت قرب أبراج اتصالات.

## حل المشاكل

**« rtl_adsb غير موجود »**
→ `sudo apt install rtl-sdr` وتأكد أن الدونغل موصول

**« usb_open error »**
→ تعريف نواة DVB-T استحوذ على الجهاز:
```bash
sudo rmmod dvb_usb_rtl28xxu rtl2832 rtl2830
echo 'blacklist dvb_usb_rtl28xxu' | sudo tee /etc/modprobe.d/blacklist-rtl.conf
```

**لا تظهر طائرات**
→ تحقق من توصيل الهوائي. جرّب `rtl_test -t` للتحقق من الدونغل.
→ تأكد من صحة `--lat` و `--lon` (ضروريان لفك تشفير الموقع).

**معدل رسائل منخفض**
→ مشكلة هوائي. انقله أعلى أو قرب نافذة.

**التطبيق يقول « تعذّر الوصول »**
→ تحقق من جدار الحماية: `sudo ufw allow 8090`
→ من جهاز آخر، استخدم IP الجهاز وليس `localhost`.
