# agymod

> Multi-account Antigravity CLI manager with automatic quota rotation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Bash](https://img.shields.io/badge/Shell_Script-121011?logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?logo=github&logoColor=white)](https://github.com/zahidoverflow/agymod)

**agymod** is a lightweight, open-source account manager for Antigravity CLI that automatically rotates between multiple Google accounts when quota limits are reached. Work uninterrupted through API rate limits with seamless account switching.

---

## 🎯 Problem

Antigravity CLI (agy) has a **~1.5 hour quota per Google account**. During extended work sessions:
- ❌ You hit quota and work stops
- ❌ Manual account switching breaks your workflow
- ❌ Managing multiple accounts is tedious
- ❌ Long sessions become impossible

## ✅ Solution

**agymod** provides:
- ✅ Automatic account rotation on quota
- ✅ One-command account setup
- ✅ Seamless token management
- ✅ Zero interruption to your workflow
- ✅ Local-only token storage (no cloud)

---

## 🚀 Quick Start

### Installation

**One-liner installation:**
```bash
sudo bash -c 'curl -fsSL https://raw.githubusercontent.com/zahidoverflow/agymod/main/agymod -o /usr/local/bin/agymod && chmod +x /usr/local/bin/agymod'
```

**Or manually:**
```bash
git clone https://github.com/zahidoverflow/agymod.git
cd agymod
chmod +x agymod
sudo cp agymod /usr/local/bin/
```

### Setup (2 minutes)

```bash
# Add your first account
agymod --add-account-auth your-email-1@gmail.com

# Add second account
agymod --add-account-auth your-email-2@gmail.com

# Add third account (optional)
agymod --add-account-auth your-email-3@gmail.com

# Verify setup
agymod --status
```

Each command handles both **adding AND authenticating** the account automatically.

### Start Using

```bash
# Interactive session (auto-rotates on quota)
agymod

# Run a single prompt
agymod "solve this challenge"

# When quota is hit, just say 'y' and it auto-switches!
Did you hit quota? (y/n)
> y
✓ Auto-rotated to next account
```

---

## 📚 Commands Reference

### Account Management

```bash
# Add and authenticate account (one command)
agymod --add-account-auth email@gmail.com

# Add account only (authenticate later)
agymod --add-account email@gmail.com

# Authenticate existing account
agymod --auth 0

# Switch to specific account
agymod --switch 1

# List all accounts
agymod --list

# Full status
agymod --status
```

### Usage

```bash
# Interactive session
agymod

# Non-interactive prompt
agymod "your prompt here"

# With explicit permission skip
agymod --dangerously-skip-permissions

# View activity logs
agymod --logs
```

### Management

```bash
# Reset everything
agymod --reset

# Show help
agymod --help
```

---

## 💡 Usage Examples

### Example 1: Long HackTheBox Challenge

```bash
$ agymod
[agymod] Using account: your-email-1@gmail.com (1/3)

> solve this challenge...
> deeper investigation...
> trying different approach...

Did you hit quota? (y/n)
> y

⚠ QUOTA REACHED - AUTO-ROTATED
Previous account: your-email-1@gmail.com
New account: your-email-2@gmail.com

To continue:
  agymod

$ agymod
[agymod] Using account: your-email-2@gmail.com (2/3)
> continue investigation...
```

### Example 2: Extended Debugging Session

```bash
# Start debugging
agymod "analyze this error..."

# Hit quota after 90 minutes
> y

# Automatically switches to next account
# Continue without interruption
```

### Example 3: CTF Competition

```bash
# Setup 5 accounts for maximum uptime
for i in {1..5}; do
  agymod --add-account-auth account-$i@gmail.com
done

# Work continuously through the competition
agymod

# Quota rotation happens automatically
# 5 × 1.5 hours = 7.5 hours of continuous work
```

---

## 🔧 How It Works

1. **Token Storage**: Each account's OAuth token is stored separately in `~/.agymod/tokens/`
2. **Token Swapping**: When you run `agymod`, it loads the current account's token
3. **Auto-Rotation**: When quota is hit and you confirm, the next account's token is loaded
4. **Complete Isolation**: Each account has its own 1.5-hour quota

```
Account 1 Token ─┐
Account 2 Token ─┼─→ [agymod] ─→ ~/.gemini/antigravity-cli/antigravity-oauth-token
Account 3 Token ─┘
                     ↓
                    [agy]
                     ↓
                  Antigravity API
```

---

## ⚙️ Requirements

- **agy** - Antigravity CLI ([install here](https://antigravity.google/))
- **bash** 4.0 or higher
- **jq** - JSON processor

### Install Dependencies

**macOS:**
```bash
brew install jq
```

**Ubuntu/Debian:**
```bash
sudo apt-get install jq
```

**Fedora/RHEL:**
```bash
sudo dnf install jq
```

---

## 📁 Configuration

agymod stores everything locally:

```
~/.agymod/
├── accounts.json          # Account registry
├── state.json            # Current state (account, rotations)
├── tokens/
│   ├── 0-token.json      # Account 1 token
│   ├── 1-token.json      # Account 2 token
│   └── 2-token.json      # Account 3 token
└── agymod.log            # Activity log
```

**All tokens stay local.** Never uploaded anywhere.

---

## 🔒 Security

- ✅ **Local Storage**: Tokens stored only in `~/.agymod/`
- ✅ **No Cloud Upload**: Your tokens never leave your machine
- ✅ **No Logging**: OAuth credentials never logged
- ✅ **Isolated Accounts**: Each account completely independent
- ✅ **Permission Control**: `.agymod/` directory has restricted permissions (700)

**Best Practices:**

```bash
# Keep .agymod directory private
chmod 700 ~/.agymod/

# Don't commit to git
echo "~/.agymod/" >> ~/.gitignore

# Treat like a password file
# Only store on trusted machines
```

---

## 🐛 Troubleshooting

### "Error: No accounts configured"

```bash
# Setup your first account
agymod --add-account-auth your-email@gmail.com
```

### "Error: Current account not authenticated"

```bash
# Re-authenticate the account
agymod --auth 0
```

### "All accounts exhausted"

Quota resets every ~1.5 hours per account. Either:
- Wait for quotas to reset
- Add more accounts with `--add-account-auth`

### agy not found

```bash
# Ensure agy is installed and in PATH
which agy
agy --version
```

### jq not found

```bash
# Install jq (see Requirements section above)
brew install jq  # macOS
sudo apt install jq  # Ubuntu/Debian
```

---

## 📊 Comparison with Alternatives

| Feature | agymod | Manual Switching | CLIProxyAPI |
|---------|--------|------------------|------------|
| Automatic Rotation | ✅ | ❌ | ✅ |
| Local Token Storage | ✅ | ✅ | ✅ |
| Simple Setup | ✅ | ✅ | ❌ (complex) |
| Works with agy directly | ✅ | ✅ | ❌ (OpenAI API only) |
| Lightweight | ✅ | ✅ | ❌ (Go binary) |
| No server needed | ✅ | ✅ | ❌ (requires server) |

---

## 📖 Documentation

- **[ABOUT.md](ABOUT.md)** - Detailed use cases and philosophy
- **[LICENSE](LICENSE)** - MIT License

---

## 🤝 Contributing

Contributions are welcome! Areas to improve:

- 🐛 Bug fixes
- ⚡ Performance improvements
- 📖 Documentation improvements
- ✨ New features
- 🧪 Test coverage

**Steps:**

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test thoroughly
5. Commit with clear messages
6. Push to your fork
7. Open a Pull Request

---

## 🎓 Learning from agymod

**agymod** is designed as a learning reference:

- **Simple**: ~250 lines of bash, easy to understand
- **Self-contained**: Single file, no dependencies beyond bash/jq
- **Well-commented**: Clear variable names and logic flow
- **Open**: Modify and adapt freely under MIT license

Perfect for learning:
- Bash scripting patterns
- OAuth token management
- CLI tool design
- JSON handling in bash

---

## 💬 Support

**Found a bug?** [Open an issue](https://github.com/zahidoverflow/agymod/issues)

**Have a feature request?** [Start a discussion](https://github.com/zahidoverflow/agymod/discussions)

**Want to contribute?** See [Contributing](#-contributing) section above

---

## 📜 License

MIT License - See [LICENSE](LICENSE) for details

```
Copyright (c) 2026 agymod contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

**You're free to:**
- Use it personally and commercially
- Modify and distribute
- Create derivatives
- Sublicense

---

## 🚀 Built With

- **Bash** - Shell scripting
- **jq** - JSON parsing
- **agy** - Antigravity CLI integration

---

## 📈 Roadmap

Future improvements under consideration:

- [ ] Config file for customization
- [ ] Quota expiration tracking
- [ ] Conversation history preservation across rotations
- [ ] Account alias support
- [ ] Integration tests
- [ ] Shell completion scripts (zsh/bash)

---

## 🌟 Why agymod?

**Before agymod:**
- ❌ Work for 90 minutes, then stuck
- ❌ Manually logout/login
- ❌ Break workflow constantly
- ❌ Impossible for long sessions

**With agymod:**
- ✅ Just ask: "Did you hit quota?"
- ✅ Say "y"
- ✅ Continue working
- ✅ Unlimited productivity

---

## 🎯 Perfect For

- 🎯 **HackTheBox Labs** - Multi-hour challenges
- 💻 **Extended Coding** - Marathon development sessions
- 🔍 **CTF Competitions** - Time-sensitive challenges
- 📚 **Research** - Deep work without interruption
- 🚀 **Production** - Debugging without limits

---

**Made with ❤️ for builders who refuse to stop**

[![Star on GitHub](https://img.shields.io/github/stars/zahidoverflow/agymod?style=social)](https://github.com/zahidoverflow/agymod)
[![Follow on GitHub](https://img.shields.io/github/followers/zahidoverflow?style=social)](https://github.com/zahidoverflow)
