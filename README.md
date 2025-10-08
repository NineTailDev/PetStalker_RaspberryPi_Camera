# PetStalker_RaspberryPi_Camera
Utilize a raspberry pi to use a webcam to watch your pets at home while you are away.


Cheapest workable setup for this project (plus off‑site Wi‑Fi‑to‑Wi‑Fi viewing):

Hardware

- Raspberry Pi Zero 2 W
- Basic UVC‑compatible USB webcam
- 16 GB Class 10 microSD card
- 5V 2A micro‑USB power supply
- Optional: simple mount/tripod

Software on the Pi

- Raspberry Pi OS (Lite is fine), Python 3
- Flask, OpenCV, numpy, imutils; apt libraries libatlas‑base‑dev, libjasper‑dev, libqtgui4, libqt4‑test, libhdf5‑dev
- Tailscale (VPN) for secure off‑site access

On your iPhone

- Safari
- Tailscale app (signed into the same account as the Pi)

Note: The original tutorial targets a Pi 4 with a Pi camera and streams to devices on the same network; the dependencies and Flask setup come from that tutorial and still apply here

. This cheaper configuration is my recommendation based on general Raspberry Pi practice.


- Raspberry Pi Zero 2 W: [https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/)
- Basic UVC‑compatible USB webcam (Logitech C270): [https://www.amazon.com/s?k=Logitech+C270+webcam](https://www.amazon.com/s?k=Logitech+C270+webcam)
- 16 GB Class 10 microSD card (SanDisk): [https://www.amazon.com/s?k=SanDisk+16GB+microSD+Class+10](https://www.amazon.com/s?k=SanDisk+16GB+microSD+Class+10)
- 5V 2A micro‑USB power supply: [https://www.amazon.com/s?k=5V+2A+micro+USB+power+supply](https://www.amazon.com/s?k=5V+2A+micro+USB+power+supply)
- Simple mount/tripod (Amazon Basics): [https://www.amazon.com/s?k=Amazon+Basics+tripod](https://www.amazon.com/s?k=Amazon+Basics+tripod)


To view the Pi’s live stream on your iPhone from another Wi‑Fi network, make the Pi reachable across networks, then open its Flask page in Safari. The tutorial’s setup is local-only (“any device on your network” on port 5000), so use a secure VPN like Tailscale so your iPhone can reach the Pi as if it’s on the same LAN

.

Steps:

- On the Raspberry Pi: install and sign in to Tailscale; start your Flask stream on port 5000 (the tutorial uses 5000)

- On your iPhone: install the Tailscale app, sign in to the same account, then open Safari and go to http://<Pi’s Tailscale IP>:5000.
- Expect a bit more latency than the ~1–2 seconds noted for local streaming


------------

Here’s a concise, updated “requirements” rewrite of the tutorial for off‑site remote viewing (wifi‑to‑wifi) and a Flask webpage that casts the livestream—no webpage code, just what you need.

**Hardware**

- Raspberry Pi 4 (recommended) or 3B+, official 5V 3A USB‑C power supply for Pi 4
- Raspberry Pi Camera Module (v2 or HQ) or a USB webcam.
- MicroSD card (32 GB, Class 10).
- Home Wi‑Fi router with internet access.
- iPhone (viewer) at your office.
- Optional: case, heatsinks/fan, tripod/mount

**Software (on the Raspberry Pi)**

- Raspberry Pi OS; enable the camera in raspi-config (Interface Options → Camera)
- Python 3.
- Flask (to serve the webpage and stream) running on port 5000 (the original tutorial uses 5000)
- Camera library: picamera2 (for modern Raspberry Pi OS) or OpenCV; choose one.
- Tailscale (VPN) for secure off‑site access across networks: install and sign in on the Pi and on your iPhone so your phone can reach the Pi as if it’s on the same LAN, then open the Flask page via the Pi’s Tailscale IP on port 5000

- Optional: systemd service to auto‑start your Flask app on boot.

**Software (on the iPhone)**

- Safari (to view the webpage).
- Tailscale app, signed into the same tailnet as the Pi.



---
Notes

Tailscale is a simple, secure VPN that links your devices into a private “tailnet” so they can reach each other as if they were on the same local network, even when they’re on different Wi‑Fi networks. The tutorial you’re using focuses on streaming to devices on the same network, not off‑site; Tailscale is what lets you view the Pi’s Flask stream from your office without port‑forwarding or extra hardware

In this project, you install Tailscale on the Raspberry Pi and on your iPhone, sign in to the same account, then open Safari to http://<Pi’s Tailscale IP>:5000 (or its MagicDNS name) to load the Flask webpage. If you’d like, I can walk you through installing it on the Pi and setting it to start automatically at boot.