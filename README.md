# TikTok Live Chat for Flipper Zero

Display your TikTok Live chat, likes, gifts and follows in real-time on your Flipper Zero via Bluetooth.

---

## How it works

```
TikTok Servers
      │
      ▼ (TikTokLive Python lib)
tiktok_server_gui.py   ←── runs on your PC
      │
      ▼ (BLE / Bluetooth serial)
Flipper Zero  ←── tiktok_live FAP
```

---

## Quick Start

### 1. Flash the Flipper app
```bash
./fbt launch APPSRC=applications_user/tiktok_live
```

### 2. Run the Python server
```bash
cd applications_user/tiktok_live
python tiktok_server_gui.py
```
Dependencies are installed automatically on first run (`TikTokLive`, `bleak`).

### 3. Connect
1. On Flipper: open the **TikTok Live** app – it starts advertising as `TikTok <name>`
2. In the Python GUI: enter the TikTok username (without `@`) and press **START**
3. The server scans for the Flipper, connects, then joins the live stream
4. Messages appear on the Flipper screen in real-time!

---

## Flipper controls

| Button | Action |
|--------|--------|
| ↑ Up | Scroll to older messages |
| ↓ Down | Scroll to newer messages |
| OK | Jump to newest message |
| Back | Exit app |

---

## Message types

| Prefix | Event |
|--------|-------|
| *(none)* | Chat comment |
| `[L]` | Like |
| `[G]` | Gift |
| `[F]` | New follower |

---

## Packet protocol

Each BLE packet is **83 bytes**:

| Offset | Size | Description |
|--------|------|-------------|
| 0 | 1 | type (0=chat, 1=like, 2=gift, 3=follow) |
| 1 | 17 | username (null-terminated, max 16 chars) |
| 18 | 65 | message (null-terminated, max 64 chars) |

---

## Credits
- [TikTok-Live-Connector](https://github.com/zerodytrash/TikTok-Live-Connector) / [TikTokLive Python](https://github.com/isaackogan/TikTokLive)
- BLE Serial helper from [Willy-JL / Xtreme-Apps](https://github.com/Flipper-XFW/Xtreme-Apps)
- App by **Dr.Mosfet**
