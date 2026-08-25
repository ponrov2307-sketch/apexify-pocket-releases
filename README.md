# Apexify SmartPulse — firmware releases

Firmware downloads for **SmartPulse Lite** and **SmartPulse Pro**.
This repository holds released binaries only; the source lives elsewhere.

---

## ⚠️ Check your model before updating

The two models take **different files**. Flashing the wrong one leaves the
screen blank and the device has to be recovered over a USB-serial cable.

| Model | Board | Screen | File to use |
|---|---|---|---|
| **SmartPulse Lite** | ESP8266 | 1.54" 240×240, no touch | `FW-SmartPulse-Lite-*.bin` |
| **SmartPulse Pro** | ESP32 (CYD) | 2.8" 320×240, touch | `FW-SmartPulse-Pro-*.bin` |

Not sure which you have? Open the device's web page — the model name is at
the top of the header, and under **Status → Technical details**.

---

## Updating over WiFi

No cable, no case opening.

1. Open the device in a browser: `http://smartpulse.local`
   (or its IP address — check your router if the name does not resolve)
2. Go to the **Update** tab
3. Choose the `.bin` file for your model
4. Upload, then wait about a minute — the device reboots itself

**Do not unplug the device while it is updating.**

Most devices can also check for updates themselves from that same tab and
install without downloading anything by hand.

---

## Verifying a download

Each version folder ships an `md5.txt`. Compare it against the file you
downloaded before flashing:

```bash
# Windows (PowerShell)
Get-FileHash -Algorithm MD5 FW-SmartPulse-Lite-v1.0.17.bin

# macOS / Linux
md5sum FW-SmartPulse-Lite-v1.0.17.bin
```

A mismatch means the download was corrupted — fetch it again rather than
flashing it.

---

## Versions

Newest first. Every version keeps its own folder, so rolling back to an
earlier build is always possible.

| Version | Notes |
|---|---|
| [v1.0.17](SmartPulse-v1.0.17/) | Lite watchlist capped at its measured ceiling of 10 symbols |
| [v1.0.16](SmartPulse-v1.0.16/) | The Lite's "Update now" button installs for real |
| [v1.0.15](SmartPulse-v1.0.15/) | **Important** — fixes WiFi updates silently doing nothing on the Lite |

Each folder contains the binaries for both models, an `md5.txt`, and an
`update_history.txt` describing what changed.

---

## If an update fails

- **The page says it uploaded but the version never changes** — this was a real
  bug on Lite units running v1.0.14 or earlier. Those devices cannot install
  any update over WiFi and need one recovery flash over a USB-serial cable;
  afterwards WiFi updates work normally. See `SmartPulse-v1.0.15/update_history.txt`.
- **The device does not come back** — unplug it, wait ten seconds, plug it in
  again. Settings and your watchlist survive an update.
- **The screen stays blank** — most likely the wrong model's file was flashed.
  Recovery needs a USB-serial adapter.
