# 📝 TIL Voice → Channel

Telegram voice message → Whisper transcription → GPT-4o formats as TIL post → publishes to channel.

## How it works

1. Send a voice message to your bot
2. Whisper transcribes it to text
3. GPT-4o formats it as a short TIL post (2-4 sentences + hashtags)
4. Posts to your Telegram channel automatically

## Setup

1. Replace `YOUR_TELEGRAM_CREDENTIAL_ID` with your Telegram bot credential
2. Replace `YOUR_BOT_TOKEN` with your bot token  
3. Replace `YOUR_OPENAI_API_KEY` with your OpenAI key
4. Replace `YOUR_CHANNEL_ID` with your channel ID (e.g. `-1001234567890`)

## Stack

- n8n Telegram Trigger
- OpenAI Whisper (speech-to-text)
- OpenAI GPT-4o (formatting)
- Telegram Bot API

## Use case

Perfect for developers who want to build a daily TIL habit — just voice a quick insight, it handles the rest.
