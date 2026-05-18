# AdGuard Home on Raspberry Pi with Docker

A complete guide to self-host **AdGuard Home** on a Raspberry Pi using Docker Compose. Block ads, trackers, and telemetry across your entire network — no need to configure every device.

---

## What you get

- Network-wide DNS-level ad blocking (browsers, apps, Smart TVs)
- Tracker and telemetry blocking
- Web UI for real-time query monitoring
- Native DNS-over-HTTPS and DNS-over-TLS
- Cosmetic filtering (hides page elements, similar to uBlock Origin)
- One-command updates

> **Does not block:** ads on YouTube and Spotify (they share the same domain as content). For that, use uBlock Origin in your browser.

---

## Requirements

- Raspberry Pi (any model running Linux)
- Docker and Docker Compose installed
- Local IP of your Raspberry Pi (e.g. `192.168.1.175`)

---

## Installation

### 1. Clone the repo

```bash
git clone https://github.com/andrmagg2001/adguard-rpi-docker.git
cd adguard-rpi-docker
```

### 2. Start the container

```bash
docker compose up -d
```

### 3. Initial setup

Open in your browser:

```
http://RASPBERRY_IP:3000
```

Follow the wizard (5 steps):
- **Step 2:** leave everything as default (All interfaces, port 80, port 53)
- **Step 3:** create a username and password
- **Steps 4/5:** informational, just click Next

### 4. Configure upstream DNS

In AdGuard → **Settings → DNS Settings → Upstream DNS servers:**

```
https://dns.cloudflare.com/dns-query
https://dns.google/dns-query
```

For more privacy:
```
https://dns.quad9.net/dns-query
```

### 5. Add blocklists

**Settings → Filters → DNS Blocklists** → Add:

| Name | URL |
|------|-----|
| AdGuard DNS filter | `https://adguardteam.github.io/HostlistsRegistry/assets/filter_1.txt` |
| AdAway | `https://adguardteam.github.io/HostlistsRegistry/assets/filter_2.txt` |
| OISD | `https://adguardteam.github.io/HostlistsRegistry/assets/filter_59.txt` |

### 6. Point your devices to AdGuard

On your **router** (if supported): set primary DNS to `RASPBERRY_IP`.

On **macOS:**
```
System Settings → Network → Wi-Fi → Details → DNS → add Raspberry IP
```

On **iPhone:**
```
Settings → Wi-Fi → (i) next to your network → Configure DNS → Manual → add Raspberry IP
```

---

## Repository structure

```
.
├── docker-compose.yml   # container configuration
└── README.md
```

The `adguard-conf/` and `adguard-work/` folders are created automatically on first run and are excluded from version control (they contain local data and credentials).

---

## Updating AdGuard Home

```bash
docker compose pull
docker compose up -d
```

---

## Troubleshooting

**Port 53 already in use:**
```bash
docker compose down --remove-orphans
docker compose up -d
```

**Check logs:**
```bash
docker logs adguardhome
```

**Verify blocking works:**
```bash
nslookup doubleclick.net RASPBERRY_IP
# Should return 0.0.0.0
```

---

## AdGuard Home vs Pi-hole

| | Pi-hole | AdGuard Home |
|---|---|---|
| Filtering | DNS only | DNS + cosmetic rules |
| DNS-over-HTTPS | External plugin | Native |
| DNS-over-TLS | External plugin | Native |
| Interface | Classic | Modern |
| Setup | Better documented | Simpler |

---
