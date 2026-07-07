# Minecraft AFK Bot

A Mineflayer-based Minecraft bot that joins an Aternos server and keeps it online 24/7 by preventing idle shutdowns.

## Stack
- **Runtime**: Node.js 20
- **Bot**: [mineflayer](https://github.com/PrismarineJS/mineflayer) + mineflayer-pathfinder
- **Web dashboard**: Express (port 5000)

## How to run
```
npm start
```
The workflow "Start application" runs this automatically. Visit the preview to see the live status dashboard.

## Configuration
All bot settings live in `settings.json`:
- `server.ip` / `server.port` — Minecraft server address
- `server.version` — Minecraft version to connect as
- `bot-account.username` — In-game display name (offline-mode servers)
- `utils.auto-auth` — `/login` password for auth-plugin servers
- `utils.anti-afk` — sneak & movement to avoid AFK kicks
- `utils.chat-messages` — periodic chat messages the bot sends
- `movement` — circle-walk, look-around, and random-jump patterns
- `discord` — optional webhook for connect/disconnect alerts

## How it works
1. Bot connects to the configured server on startup.
2. If the server is offline or connection drops, the bot waits and retries (exponential backoff up to `max-reconnect-delay`).
3. Anti-AFK routines (sneaking, movement, chat) run while connected.
4. Express server on port 5000 serves the dashboard and a `/health` endpoint.
5. On Render.com, set `RENDER_EXTERNAL_URL` to enable the self-ping keep-alive.

## User preferences
