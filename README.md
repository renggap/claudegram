# Claudegram

A Telegram bot that bridges messages to Claude Code running on your local machine, providing full agent capabilities (Bash, Read, Write, Edit, etc.) via Telegram.

## Architecture

```
Telegram App → Telegram API → Claudegram Bot → Claude Agent SDK → Local Machine
```

## Features

### Core
- 🤖 Full Claude Code agent capabilities via Telegram
- 💬 Real-time streaming responses
- 📁 Project-based sessions with persistence
- 🔐 User whitelist authentication

### Enhanced UX (v2.0)
- 📋 **Command Menu** - Auto-suggest commands in Telegram's menu
- ✨ **Two-Step Commands** - Interactive ForceReply prompts with placeholders
- 📄 **Telegraph Integration** - View markdown files with Instant View
- 📎 **File Downloads** - Send any project file as attachment
- 🎨 **MarkdownV2 Formatting** - Properly rendered responses
- 📊 **Smart Message Chunking** - Handles long responses with code block preservation

## Setup

### 1. Create a Telegram Bot
- Open [@BotFather](https://t.me/botfather) in Telegram
- Send `/newbot` and follow the instructions
- Copy the bot token

### 2. Register Commands with BotFather (Optional but Recommended)
Send this to BotFather after selecting your bot with `/setcommands`:
```
start - 🚀 Show help and getting started
project - 📁 Set working directory
status - 📊 Show current session status
clear - 🗑️ Clear conversation history
cancel - ⏹️ Cancel current request
file - 📎 Download a file from project
telegraph - 📄 View markdown with Instant View
model - 🤖 Switch AI model
mode - ⚙️ Toggle streaming mode
plan - 📋 Start planning mode
explore - 🔍 Explore codebase
loop - 🔄 Run in loop mode
sessions - 📚 View saved sessions
resume - ▶️ Resume a session
commands - 📜 List all commands
```

### 3. Get Your Telegram User ID
- Open [@userinfobot](https://t.me/userinfobot) in Telegram
- It will send you your user ID

### 4. Configure Environment
```bash
cp .env.example .env
```
Edit `.env` with your values:
```bash
TELEGRAM_BOT_TOKEN=your_bot_token
ALLOWED_USER_IDS=your_user_id
ANTHROPIC_API_KEY=your_anthropic_key  # Optional if using Claude Max
WORKSPACE_DIR=/path/to/your/projects  # Default workspace for projects
```

### 5. Install & Run
```bash
npm install
npm run dev
```

## Commands

### Session Management
| Command | Description |
|---------|-------------|
| `/start` | Welcome message and help |
| `/project` | Set working directory (interactive) |
| `/newproject <name>` | Create and open a new project |
| `/clear` | Clear session (with confirmation) |
| `/status` | Show current session info |
| `/sessions` | List all saved sessions |
| `/resume` | Pick from recent sessions |
| `/continue` | Resume most recent session |

### Claude Modes
| Command | Description |
|---------|-------------|
| `/plan` | Enter plan mode for complex tasks |
| `/explore` | Explore codebase to answer questions |
| `/loop` | Run iteratively until task complete |
| `/model` | Switch between sonnet/opus/haiku |
| `/mode` | Toggle streaming/wait mode |

### File Operations
| Command | Description |
|---------|-------------|
| `/file` | Download a file from project |
| `/telegraph` | View markdown with Instant View |

### Utility
| Command | Description |
|---------|-------------|
| `/ping` | Check if bot is responsive |
| `/cancel` | Cancel current request |
| `/commands` | Show all available commands |

## Configuration

| Variable | Description | Default |
|----------|-------------|---------|
| `TELEGRAM_BOT_TOKEN` | Bot token from BotFather | Required |
| `ALLOWED_USER_IDS` | Comma-separated user IDs | Required |
| `ANTHROPIC_API_KEY` | Anthropic API key | Optional (uses Claude Max if not set) |
| `WORKSPACE_DIR` | Default workspace for projects | Required |
| `STREAMING_MODE` | `streaming` or `wait` | `streaming` |
| `STREAMING_DEBOUNCE_MS` | Update debounce in ms | `500` |
| `MAX_MESSAGE_LENGTH` | Max Telegram message length | `4000` |
| `DANGEROUS_MODE` | Auto-approve all tool permissions | `false` |
| `MAX_LOOP_ITERATIONS` | Max iterations for /loop | `5` |

## Telegraph Integration

For long markdown files or content with tables, Claudegram uses [Telegraph](https://telegra.ph) to create Instant View pages:

- Automatic for responses > 2500 chars or containing tables
- Manual via `/telegraph <file>` command
- Supports: headers, lists, code blocks, bold, italic, links, strikethrough
- Creates permanent URLs viewable in Telegram's Instant View

## Development

```bash
# Run in development mode with hot reload
npm run dev

# Type check
npm run typecheck

# Build for production
npm run build

# Run production build
npm start
```

## Security

- Only configured user IDs can interact with the bot
- Claude operates within the specified working directory
- Uses `acceptEdits` permission mode for file operations
- `DANGEROUS_MODE` auto-approves all permissions (use with caution)

## Platform Support

- **macOS**: Full support including sleep prevention
- **Linux**: Full support (tested on Debian 12)
- **Windows**: Should work (untested)

## Credits

Original project by [NachoSEO](https://github.com/NachoSEO/claudegram)

Enhanced features contributed by the community.

## License

MIT
