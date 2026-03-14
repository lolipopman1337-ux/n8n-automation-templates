# Daily Bot Monitor

Every morning sends a status report to Telegram listing which n8n workflows are active and which are not.

## Node Schema

```
Schedule Trigger (CRON 9am)
  -> HTTP Request (GET /api/v1/workflows via n8n API)
  -> Code (filter active/inactive, build report text)
  -> Telegram sendMessage
```

## Setup

1. **Import** `daily-bot-monitor.json` into n8n.

2. **n8n API credential** - create an `HTTP Header Auth` credential:
   - Header name: `X-N8N-API-KEY`
   - Value: your n8n API key (Settings > API Keys)

3. **Replace placeholders** in the workflow:

   | Placeholder | Replace with |
   |---|---|
   | `YOUR_N8N_BASE_URL` | e.g. `https://your-n8n.domain` |
   | `YOUR_N8N_API_CREDENTIAL_ID` | ID of the credential you created above |
   | `YOUR_TELEGRAM_CHAT_ID` | your Telegram chat/user ID |
   | `YOUR_TELEGRAM_CREDENTIAL_ID` | ID of your Telegram Bot credential |

4. **CRON schedule** - default is `0 9 * * *` (9:00 AM server time). Change in Schedule Trigger node.

5. **Activate** the workflow.

## Example Report

```
Daily Bot Monitor Report
2024-03-15

Active: 3
  - Dietitian Bot
  - City59 Auto-Post
  - Error Notifier

Inactive: 2
  - Old Campaign
  - Test Workflow

Total: 5
```
