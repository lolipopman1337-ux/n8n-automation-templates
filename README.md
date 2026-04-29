# n8n Automation Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![n8n](https://img.shields.io/badge/built%20with-n8n-EA4B71?logo=n8ndotio&logoColor=white)](https://n8n.io)
[![Telegram Bot API](https://img.shields.io/badge/Telegram-Bot%20API-26A5E4?logo=telegram&logoColor=white)](https://core.telegram.org/bots/api)
[![OpenAI](https://img.shields.io/badge/LLM-OpenAI-412991?logo=openai&logoColor=white)](https://platform.openai.com)
[![Supabase](https://img.shields.io/badge/DB-Supabase-3ECF8E?logo=supabase&logoColor=white)](https://supabase.com)

Production-tested n8n workflow templates for Telegram bots, multi-agent AI orchestration, and operational automation. Import the JSON, wire up your credentials, and you have a running system in minutes.

Each folder is self-contained: workflow JSON + a README explaining what it does, the architecture, and how to adapt it.

---

## Templates

| Folder | What it does | Pattern |
|---|---|---|
| [`n8n-multi-agent-orchestrator/`](./n8n-multi-agent-orchestrator) | Six-workflow hub: a Telegram bot that routes inbound messages through an LLM classifier to specialised sub-agents (Action / Media / Commands / Qualifier) | Multi-agent routing, structured output, executeWorkflow chaining |
| [`telegram-voice-to-post/`](./telegram-voice-to-post) | Voice messages → Whisper transcription → AI-rewritten Telegram channel post | Voice ingest, ASR, content pipeline |
| [`til-voice-to-channel/`](./til-voice-to-channel) | "Today I Learned" voice notes → daily digest auto-published to a TG channel | Voice ingest, scheduling, summarisation |
| [`daily-bot-monitor/`](./daily-bot-monitor) | Cron-based health-check across all active workflows; reports liveness via Telegram | Operational reliability, dead-man-switch |
| [`error-notifier/`](./error-notifier) | Global n8n error trigger → categorises and routes alerts to the right channel | Global error handling, observability |

---

## Architecture patterns demonstrated

- **Routing as its own workflow** — keep the classifier auditable and A/B-able without touching downstream agents (`n8n-multi-agent-orchestrator/02_ai_classifier.json`)
- **Structured output, not free text** — every routing decision uses LangChain's `outputParserStructured` so downstream nodes get a typed payload
- **`executeWorkflow` over webhook chains** — transactional invocations, no inter-workflow HTTP timeouts
- **Single audit row per inbound** — capture → classify → action all stamp the same DB row, so an end-to-end debug is one SQL query
- **Dead-man-switch monitoring** — the health-check is itself monitored, because silent monitor failure is the worst monitor failure
- **Graceful degradation** — every external dependency (Telegram, Supabase, OpenAI) has explicit fallbacks instead of swallowed errors

---

## How to use

1. **Clone or download** this repo.
2. **In n8n:** `Workflows → Import from file → select the .json`. Multi-file templates (like the orchestrator) need to be imported in dependency order — see the folder's README.
3. **Create credentials** in n8n for the services the workflow uses (Telegram, OpenAI, Supabase, etc.). The JSON files reference credentials by *type* — IDs are placeholders that you'll re-link in the UI after import.
4. **Update placeholders** in the workflow body (`<BOSS_USER_ID>`, `<webhook-uuid>`, etc.) — search the JSON before activating.
5. **Activate** and watch the executions tab.

---

## Stack

- **n8n** self-hosted (Docker) — primary orchestrator
- **OpenAI** (`gpt-4o`, `whisper-1`) — model layer; trivially swappable for Anthropic / Mistral / local via the `lmChat*` nodes
- **Telegram Bot API** — primary surface
- **Supabase** (Postgres) — persistence + audit trail
- **LangChain n8n nodes** (`@n8n/n8n-nodes-langchain`) — agent + structured output

---

## Sanitisation

All workflows in this repo are exported from production and **sanitised**:
- No bot tokens, API keys, or JWTs (n8n keeps those in credentials, not in workflow JSON)
- No real chat IDs, user IDs, emails, phone numbers, or internal URLs
- Webhook UUIDs replaced with `<webhook-uuid>` placeholders (n8n regenerates on import)
- Credential references neutralised — you re-link in the UI

If you spot anything that looks sensitive, please open an issue and I'll patch it.

---

## License

MIT — see [LICENSE](LICENSE). No warranty; you wire it up to your stack.

Pull requests with new templates or improvements welcome.
