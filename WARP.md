# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

MemeStash is a Discord bot written in Python that fetches and serves memes on demand. The bot responds to the `$meme` command by retrieving random memes from the meme-api.com API and posting them to Discord channels.

## Development Commands

### Setup and Installation
```bash
# Install required dependencies
python3 -m pip install discord.py python-dotenv requests

# Set up environment variables
# Ensure .env file contains: DISCORD_TOKEN="your_discord_bot_token_here"
```

### Running the Bot
```bash
# Run the Discord bot
python3 bot.py
```

### Testing Connection
```bash
# Test if all imports work correctly
python3 -c "import discord, requests, json, os; from dotenv import load_dotenv; print('All dependencies available')"
```

### Development Workflow
```bash
# Check git status
git status

# View recent commits
git --no-pager log --oneline -5

# Clean Python cache files
rm -rf __pycache__/
```

## Architecture

### Code Structure
- **Single-file architecture**: All bot logic is contained in `bot.py` (30 lines)
- **Simple command pattern**: Uses message content parsing with `startswith('$meme')`
- **API integration**: Direct HTTP requests to meme-api.com using `requests` library
- **Environment-based configuration**: Discord token stored in `.env` file

### Key Components

#### MyClient Class (discord.Client)
- `on_ready()`: Logs when bot successfully connects
- `on_message()`: Handles incoming messages and responds to `$meme` commands

#### get_meme() Function
- Makes GET request to `https://meme-api.com/gimme`
- Parses JSON response and extracts image URL
- Returns meme URL string

### Dependencies
- `discord.py`: Discord API wrapper
- `python-dotenv`: Environment variable management
- `requests`: HTTP client for API calls
- Standard library: `json`, `os`

## Environment Requirements

### Discord Bot Setup
- Bot requires `message_content` intent enabled
- Discord token must be stored in `.env` file as `DISCORD_TOKEN`
- Bot should have appropriate permissions in Discord server (Send Messages, Read Messages)

### Python Version
- Compatible with Python 3.13+
- No complex dependencies or version conflicts

## Security Notes

- **Token Security**: Discord token is stored in `.env` file (excluded from git)
- **API Reliability**: Bot depends on external meme-api.com service availability
- **Error Handling**: Minimal error handling - API failures will cause bot crashes

## Bot Behavior

### Commands
- `$meme`: Fetches and posts a random meme image URL

### Response Pattern
- Responds only in channels where command is typed
- Ignores messages from itself to prevent loops
- No rate limiting or spam protection implemented