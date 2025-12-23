# 🛡️ Network Traffic Monitor

A cross-platform Python tool that monitors incoming network traffic and alerts via Discord when traffic exceeds defined thresholds, with optional packet capture for diagnostics and analysis.

**Screenshot Showcase**

<img width="443" height="224" alt="image" src="https://github.com/user-attachments/assets/6017c1e3-0916-4ec4-84f6-facf159f9b22" />

*PPS threshold altered strictly for this example*


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

**Creating a Discord webhook**



**Have admin permissions and select settings for the desired output channel**

<img width="382" height="81" alt="image" src="https://github.com/user-attachments/assets/8fedfefe-7142-4b19-902e-6bbf475bd8dd" />


**Select integrations**

<img width="296" height="256" alt="image" src="https://github.com/user-attachments/assets/a4bdeede-db9d-4ae0-aead-1f805cd70b84" />


**Webhook**

<img width="1114" height="441" alt="image" src="https://github.com/user-attachments/assets/6665b2ec-b8d3-442e-b829-e4748e0d32b5" />


**New Webhook**

<img width="1112" height="270" alt="image" src="https://github.com/user-attachments/assets/66701e34-1cc4-4514-b127-89cd18fb658b" />


**Copy Webhook URL and add to the script**

<img width="678" height="215" alt="image" src="https://github.com/user-attachments/assets/8db71527-33e3-4d29-8d2d-a6806d8187c5" />







---

## 🔡 Server Variables

These are the main configurable variables at the top of the script:

```py
SERVER_NAME = "AWS, France"
PPS_THRESHOLD = 50000
CHECK_INTERVAL = 1
CAPTURE_PACKET_COUNT = 10000
CAPTURE_FILENAME_PREFIX = "traffic_capture_"
```

---
