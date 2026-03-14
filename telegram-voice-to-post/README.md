# Telegram Voice to Post

Send a voice message to your Telegram bot and get a formatted post published to your channel automatically. Transcription via Whisper, formatting via GPT-4o.

## Node Schema

```
Telegram Trigger (voice message)
  -> Telegram getFile (get file_path)
  -> HTTP Download (download OGG audio)
  -> Whisper API (transcribe to text)
  -> GPT-4o (format as channel post)
  -> Telegram sendMessage (publish to channel)
```

## Setup

1. **Import** `telegram-voice-to-post.json` into n8n.

2. **Create a Telegram Bot** via @BotFather if you don't have one. Add it as admin to your channel.

3. **Replace placeholders**:

   | Placeholder | Replace with |
   |---|---|
   | `YOUR_BOT_TOKEN` | Telegram bot token from BotFather |
   | `YOUR_CHANNEL_ID` | Channel ID, e.g. `-1001234567890` |
   | `YOUR_OPENAI_KEY` | OpenAI API key |
   | `YOUR_TELEGRAM_CREDENTIAL_ID` | n8n Telegram credential ID |
   | `YOUR_WEBHOOK_ID` | Auto-assigned when you activate |

4. **Activate** the workflow - n8n registers the webhook with Telegram automatically.

5. **Test**: send a voice message to your bot. The formatted post should appear in the channel within seconds.

## Notes

- Only processes `message.voice` updates. Add an IF node to handle text messages if needed.
- GPT-4o system prompt can be customized in the "GPT-4o Format Post" node to match your channel tone.
- Whisper supports 57 languages - transcription language is auto-detected.
- Audio files are not stored; they are streamed directly to the Whisper API.
