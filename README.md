# n8n Automation Templates

Ready-to-use n8n workflow templates for Telegram bots, AI agents, and business automation.

Built and battle-tested in production. Just import, configure credentials, and run.

---

## Templates

### Telegram Bots
| Template | Description |
|----------|-------------|
| `telegram-ai-bot` | AI assistant with GPT-4o, voice messages, conversation memory |
| `telegram-digest-bot` | Daily digest with personalized summaries |
| `telegram-callback-router` | Inline keyboard handler with callback routing |

### Social Media Autoposter
| Template | Description |
|----------|-------------|
| `vk-autoposter` | Auto-post from RSS/VK groups to your channel |
| `telegram-channel-autoposter` | Curate and repost content with AI filtering |

### AI Agents
| Template | Description |
|----------|-------------|
| `copywriting-agent` | AI agent that writes posts, captions, ads on demand |
| `lead-qualifier` | Qualifies leads via Telegram, saves to CRM |

### Utilities
| Template | Description |
|----------|-------------|
| `error-notifier` | Global error handler — alerts on failed workflows |
| `daily-bot-monitor` | CRON: checks all active bots, reports status |

---

## How to Use

1. Download the `.json` file
2. In n8n: **Workflows → Import from file**
3. Configure credentials
4. Activate

---

## Stack

- **n8n** self-hosted (Docker)
- **OpenAI** gpt-4o / whisper-1
- **Telegram Bot API**
- **Supabase** (PostgreSQL)

---

## Author

Automation developer. Building AI-powered bots and workflows.

Open for freelance — Telegram: @choppacrypto

---

MIT License
