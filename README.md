# TRPG Desk · TRPG Game Master Assistant

> A web-based real-time multiplayer Tabletop RPG (TRPG) assistant. No app install required — host runs it on a computer, players scan a QR code with their phones to join.

[English](./README.md) · [简体中文](./README.zh-CN.md)

## ✨ Features

- **Real-time multiplayer board & tokens** — Host uploads a map background, drags NPC/clue/event markers; player tokens sync in real time on the big screen. Supports turn-based rounds, HP display, map pings.
- **AI-powered NPC dialogue & image generation** — One-click AI generation of map backgrounds, NPC portraits, item icons. NPCs support multi-turn AI dialogue (with personality, memory, opening line, and goal). Pluggable Agnes AI or any OpenAI-compatible API.
- **NPC shop + clue cards + inventory system** — Host configures shop items for NPCs (gold 🪙 + stock 📦); players buy in real time from their phones. Clue cards can be pushed to specific players' inventories.
- **Cross-platform, zero-install** — Pure browser. Host on computer, players on phones, public board on tablet/TV. Just need a shared Wi-Fi.
- **Bilingual (Chinese / English)** — Visit `/` for Chinese, `/en` for English. Players in the same room can use different languages.

## 🚀 Quick Start

### Option A: One-click release package (recommended for non-developers)

Download the latest release for your platform:

- **Windows**: `trpg-desk-v2.4.51-windows.zip` → unzip → double-click `start.bat`
- **macOS**: `trpg-desk-v2.4.51-mac.tar.gz` → unzip → double-click `start.command`

Requirements:
- Windows: Node.js 18+ installed ([download](https://nodejs.org/))
- macOS: Node.js 18+ installed (`brew install node`)

The script will:
1. Install npm dependencies automatically
2. Start the server on port 3000
3. Open your default browser at http://localhost:3000/

### Option B: From source

```bash
git clone https://github.com/<your-username>/trpg-desk.git
cd trpg-desk
npm install
npm start
```

Then open http://localhost:3000/ in your browser.

## 🎲 How to Use

1. **Host**: Open the URL on your computer, pick "Game Master" role. Use the console to upload maps, place NPCs, manage turns.
2. **Players**: Scan the QR code shown on the host screen, or visit the LAN URL on their phones. Pick a player slot.
3. **Big screen (optional)**: Open the URL on a tablet/TV, pick "Pad Board". Displays the public map with real-time token movements.

## 🔧 Configuration (AI features)

Copy `config.example.json` to `config.json` and edit:

```json
{
  "agnesApiKey": "sk-your-agnes-api-key-here",
  "customApi": {
    "enabled": false,
    "baseUrl": "https://api.openai.com",
    "apiKey": "sk-your-openai-key",
    "textModel": "gpt-4o-mini",
    "imageModel": "dall-e-3",
    "imageSize": "1024x1024"
  }
}
```

- **Default**: Uses [Agnes AI](https://agnes-ai.com) (`agnes-2.0-flash` text, `agnes-image-2.1-flash` image).
- **Custom**: Set `customApi.enabled: true` and provide your OpenAI / DeepSeek / Qwen / any OpenAI-compatible API key. The image model defaults to `dall-e-3`, text to `gpt-4o-mini`.
- **Priority**: Environment variable `AGNES_API_KEY` > `config.json` > `config.example.json`.

## 🌍 Language / Bilingual Support

| URL | Language |
| --- | --- |
| `http://localhost:3000/` | 中文 (Simplified Chinese) |
| `http://localhost:3000/en` | English |

Players in the same room can each pick their preferred language — both versions share the same backend, sockets, and data.

## 📦 Deployment

Beyond the one-click packages, the project supports:

- **PM2**: `pm2 start ecosystem.config.js`
- **Docker**: `docker-compose up -d`
- **Nginx reverse proxy**: forward to port 3000

See `DEPLOY.md` for details.

## 🛠️ Tech Stack

- **Backend**: Node.js + Express + Socket.IO + Multer
- **Frontend**: Vanilla JavaScript + WebSocket + Web Speech API
- **AI**: Agnes AI or any OpenAI-compatible API
- **Real-time sync**: Socket.IO rooms (single-room model)

## 📁 Project Structure

```
trpg-desk/
├── server.js              # Express + Socket.IO server
├── public/
│   ├── index.html         # Chinese UI
│   ├── client.js          # Chinese client logic
│   ├── style.css          # Shared styles
│   └── en/
│       ├── index.html     # English UI
│       └── client.js       # English client logic
├── config.example.json    # Configuration template
├── config.json            # (User-created) runtime config
├── uploads/               # AI-generated images & uploaded files
├── ecosystem.config.js    # PM2 config
├── Dockerfile             # Docker image
└── docker-compose.yml     # Docker Compose
```

## 📜 License

MIT — feel free to use, modify, and distribute. Designed for tabletop game stores, TRPG communities, and educators.

## 🙏 Acknowledgements

- [Agnes AI](https://agnes-ai.com) — default AI provider
- [Socket.IO](https://socket.io) — real-time communication
- Built entirely with [TRAE IDE](https://www.trae.cn/) + AI-assisted development across 10+ iterations.
