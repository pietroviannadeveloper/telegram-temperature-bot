#  Telegram Temperature Bot (n8n + Gemini)

A Telegram bot built with **n8n** that responds with the current temperature of a requested city.

The bot uses:

- Telegram Trigger
- AI Agent
- Google Gemini Chat Model

The AI model handles city detection and temperature lookup directly.

---

##  How It Works

1. A user sends a message in Telegram asking for a city's current temperature.
2. The AI Agent processes the request.
3. Gemini retrieves the current temperature.

## 🛠Requirements

- n8n (self-hosted or cloud)
- Telegram Bot Token (via BotFather)
- Google Gemini API credentials configured in n8n
