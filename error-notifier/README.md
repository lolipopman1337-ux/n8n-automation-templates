# Error Notifier

Global error handler for n8n — catches any failed workflow and sends a Telegram alert with error details + direct link to the execution.

## Flow

`Error Trigger` → `Format Message` → `Send Alert (Telegram)`

## Setup

1. Import `error-notifier.json` into n8n
2. In **Format Message** node: replace `YOUR_N8N_URL` with your n8n URL
3. In **Send Alert** node: replace `YOUR_BOT_TOKEN` and `YOUR_CHAT_ID`
4. Activate — it now watches ALL your other workflows

## Alert looks like

```
Error: My Workflow Name
Node: HTTP Request
Connection refused: https://api.example.com

Execution: https://your-n8n.com/workflow/abc/executions/123
```

## Notes

- One workflow = global error monitoring for everything
- Plain HTTP Request node (no Telegram credential needed)
- Error truncated to 300 chars to avoid Telegram limits
