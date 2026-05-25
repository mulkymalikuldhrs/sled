# Sled 🛷

Use your desktop Claude Code, Codex or Gemini CLI coding agent from your phone. With voice.

<p align="center">
  <img src="https://assets.layercode.com/mockup.gif" alt="Sled demo" width="400">
</p>

> **This is experimental software.** Like an actual sled: fast and fun, but if you're not careful, you can crash into a tree.

## Why

Coding agents need input every 10-60 minutes. If you're not at your desk, they just sit there.

Typing on a phone is slow. Voice is fast.

Terminals can't do two-way voice. Sled runs in the browser.

That's why Sled exists.

## Supported Agents

| Agent | Status |
|-------|--------|
| Claude Code | ✔ |
| OpenAI Codex | ✔ |
| Gemini CLI | ✔ |

## Install

Clone the repo:

```bash
git clone https://github.com/layercodedev/sled
cd sled
```

Then setup:

```bash
pnpm install
pnpm migrate
```

## Setup

You need a coding agent installed:

```bash
# Claude Code
npm install -g @anthropic-ai/claude-code@latest
# You also need Agent Control Protocol adapter
npm install -g @zed-industries/claude-code-acp

# Codex
npm install -g @openai/codex
# You also need Agent Control Protocol adapter
npm install -g @zed-industries/codex-acp

# Gemini CLI
npm install -g @google/gemini-cli@latest
# Gemini supports Agent Control Protocol natively
```

Start Sled:

```bash
pnpm start
```

Open **http://localhost:8787** in your browser.

## Usage

### Talk to your agent

Open Sled on your desktop or phone. Tap 'Enable Voice Mode'. Say what you want. Then hit the send message button or press enter.

```
"Add dark mode to the settings page"
```

Sled transcribes and sends it to your agent.

### Hear the response

Your agent works. When it's done, you hear what it did.

```
"I've added a toggle in SettingsPage.tsx and created a ThemeContext.
Want me to add the CSS variables too?"
```

## Remote Mobile Access

> **⚠️ Secure your tunnel.** If you expose your machine without proper authentication (e.g. ngrok without `--basic-auth`), anyone can control your entire computer. Coding agents can run commands, read files, and more. Use strong passwords.

### Tailscale (Recommended)

Install [Tailscale](https://tailscale.com) on your computer and phone. Access Sled over your private network. No ports exposed.

### ngrok (Quick Setup)

```bash
ngrok http 8787 --basic-auth="user:password"
```

Use a strong password. This exposes your machine to the internet.

## How It Works

```
┌─────────────┐                    ┌──────────────┐                    ┌─────────────┐
│   Phone     │ ◄───Tailscale────► │    Sled      │ ◄───ACP──────────► │ Claude Code │
│  (browser)  │                    │  (your Mac)  │                    │    Codex    │
│             │                    │              │                    │    Gemini   │
└─────────────┘                    └──────────────┘                    └─────────────┘
```

1. **You talk** — Sled transcribes and sends it to your agent
2. **Agent works** — Runs locally on your computer. Code never leaves your machine.
3. **You hear back** — Response converted to speech

## Features

- **Voice input** — Talk instead of type. Handles camelCase and function names.
- **Voice output** — Responses read aloud. 300+ voices.
- **Notifications** — Agent finishes or needs input. You get a ping.
- **Session resume** — Pick up where you left off.
- **Code stays local** — Your agent runs on your machine. Nothing leaves.

## Tech Stack

- [Hono](https://hono.dev) — Web framework
- [Cloudflare Workers](https://workers.cloudflare.com) — Runtime (local via Wrangler)
- [Durable Objects](https://developers.cloudflare.com/durable-objects/) — Stateful WebSocket handling
- [HTMX](https://htmx.org) — Real-time UI

## Optional Configuration

Sled reads runtime options from environment variables (e.g. `.dev.vars` or `wrangler.jsonc`).

- `DISABLE_VOICE_MODE` (optional): Set to any non-empty value other than `false` to disable voice mode and all connections to layercode.com's voice API. Leave unset/empty/`false` to keep voice mode enabled.

## Data Privacy

Audio and agent responses are sent through [Layercode](https://layercode.com) for voice processing (not stored). You can disable voice output in settings to keep responses local.

## License

[MIT License](LICENSE) © Layercode

---

## 📬 Contact

**Mulky Malikul Dhaher** — [mulkymalikuldhaher@email.com](mailto:mulkymalikuldhaher@email.com)

GitHub: [https://github.com/mulkymalikuldhrs](https://github.com/mulkymalikuldhrs)

---

## ⚠️ Disclaimer

**This project is for Education Purpose only.**

All content, code, and documentation provided in this repository are intended solely for educational and research purposes. Nothing in this repository constitutes financial, investment, legal, or professional advice.

Use at your own risk. The authors and contributors assume no liability for any losses, damages, or consequences arising from the use of this software or information provided herein.
