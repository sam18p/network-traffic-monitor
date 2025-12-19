# 🛡️ Network Traffic Monitor

A cross-platform Python tool that monitors incoming network traffic and alerts via Discord when traffic exceeds defined thresholds, with optional packet capture for diagnostics and analysis.

---

## 📑 Table of Contents
1. [Features](#-features)
2. [Requirements](#-requirements)
3. [Installation](#-installation)
4. [How to Run](#️-how-to-run)
   - [Windows](#-windows)
   - [macOS](#-macos)
   - [Linux](#-linux)
5. [How to Deploy on a Server](#-how-to-deploy-on-a-server)
   - [Windows](#-windows-server)
   - [macOS](#-macos-server)
   - [Linux](#-linux-server)
6. [Configuring the Discord Webhook](#-discord-webhook)
7. [Configuring Server Variables](#-server-variables)
---

## ⭐ Features

- Cross-platform (Linux, Windows, macOS)
- Real-time monitoring of incoming packets per second
- Configurable traffic thresholds
- Discord webhook alerts with relevant context
- Optional packet capture for investigation and diagnostics
- Designed to run quietly in the background


---

## 📦 Requirements

- Python **3.8+**
- Works on:
  - Windows 10/11
  - macOS (Intel & Apple Silicon)
  - Linux distributions (Ubuntu, Debian, Fedora, Arch, etc.)

---

## 📥 Installation

```bash
git clone https://github.com/sam18p/network-traffic-monitor.git
cd network-traffic-monitor
```

## ▶️ How to Run

The script is a single Python file — running it is mostly the same on all systems.

## 🪟 Windows

Check Python version:

python --version


Run the tool:

python network-traffic-monitor.py


If that fails, try:

py network-traffic-monitor.py

## 🍎 macOS

Verify Python3:

python3 --version


Run the script:

python3 network-traffic-monitor.py


If Python isn’t installed:

brew install python

## 🐧 Linux

Most Linux distros come with Python preinstalled.

Run the script:

python3 network-traffic-monitor.py


If Python is missing:

Debian/Ubuntu:

sudo apt install python3


Fedora:

sudo dnf install python3


Arch:

sudo pacman -S python

---

## 🌐 How to Deploy on a Server

The script is a single Python file — running it is mostly the same on all systems.

## 🪟 Windows Server

Check Python version:

python --version


**Option 1: Simple detached run (console hidden)**

pythonw network-traffic-monitor.py

**Option 2: Run in background with output logged (from Command Prompt)**

start /B python network-traffic-monitor.py > monitor.log 2>&1



If that fails, try:

py network-traffic-monitor.py

## 🍎 macOS Server

```bash
As of April 21, 2022, Apple has discontinued macOS Server. Existing macOS Server customers can continue to download and use the app with macOS Monterey.
```
Read more on [Apple's Website](https://support.apple.com/en-us/101601)

Verify Python3:

python3 --version

nohup python3 network-traffic-monitor.py > monitor.log 2>&1 &

You can also use **screen** or **tmux** if you prefer an attachable session:

screen -dmS monitor python3 network-traffic-monitor.py


## 🐧 Linux Server

Most Linux distros come with Python preinstalled.

nohup python3 network-traffic-monitor.py > monitor.log 2>&1 &

To check if it's running:

ps aux | grep network-traffic-monitor.py

To stop it:

pkill -f network-traffic-monitor.py

---

## 🪝 Discord Webhook

To receive alerts, create a Discord webhook in your server channel settings (Integrations → Webhooks → New Webhook). Copy the webhook URL and replace the placeholder in the script:

```py
DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN"
```

The script sends rich embeds with a red alert color, server name, incoming PPS, and (after capture) a note about the saved **.pcap** file.


---

## 🔡 Server Variables

These are the main configurable variables at the top of the script:

```py
SERVER_NAME = "AWS, France"
PPS_THRESHOLD = 50000
CHECK_INTERVAL = 1
CAPTURE_PACKET_COUNT = 10000
CAPTURE_FILENAME_PREFIX = "attack_capture_"
```

**Why 50,000 PPS as the default threshold?**

According to Cloudflare's 2025 Q2 DDoS Threat Report, around 85% of observed Layer 3/4 (network-layer) DDoS attacks did not exceed 50,000 packets per second (PPS). This means 50k PPS is above the vast majority of typical attacks while still being a conservative early-warning level for unprotected servers (e.g., most VPS setups can handle 100k–500k PPS before major issues, but smaller floods can still cause disruption).
  -It's a good starting point for smaller servers or early detection.
  -For high-traffic sites (e.g., gaming/streaming), raise it to 100,000–200,000 PPS to avoid false positives.
  -Source: [Cloudflare DDoS Threat Report for 2025 Q2](https://blog.cloudflare.com/ddos-threat-report-for-2025-q2/)

Adjust these values based on your server's normal traffic baseline for best results!

---
