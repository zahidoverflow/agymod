# agymod - Antigravity CLI Multi-Account Proxy

A multi-account manager for **Antigravity CLI (agy)** with automatic quota rotation. Switch between multiple Google accounts seamlessly and auto-rotate when quota limits are reached.

## Features

✅ **Multiple Account Management** - Add and manage up to N Antigravity accounts  
✅ **Token Isolation** - Each account's OAuth token stored separately  
✅ **Auto-Rotation** - Automatically switch to next account when quota is hit  
✅ **One-Command Setup** - Add and authenticate in a single command  
✅ **Manual Control** - Switch accounts manually anytime  
✅ **Activity Logging** - Track all account switches and rotations  

## Installation

```bash
# Clone or download agymod
git clone <your-github-repo> agymod
cd agymod

# Make executable
chmod +x agymod

# Add to PATH (optional)
sudo cp agymod /usr/local/bin/
```

## Quick Start

### Setup (One command per account)
```bash
agymod --add-account-auth yakisec@gmail.com
agymod --add-account-auth kirucianaz@gmail.com
agymod --add-account-auth groksec@gmail.com
```

Each command:
1. Adds the account to the config
2. Opens `agy` for OAuth authentication
3. Saves the OAuth token securely

### Use It

```bash
# Interactive session (auto-rotates on quota)
agymod

# Run single prompt
agymod "solve this ctf challenge"

# Check status
agymod --status
```

### When Quota is Hit

```bash
$ agymod
[agymod] Using account: yakisec@gmail.com (1/3)
> hello

Did you hit quota? (y/n)
> y

⚠ QUOTA REACHED - AUTO-ROTATED
Previous account: yakisec@gmail.com
New account: kirucianaz@gmail.com

To continue:
  agymod  # Use next account
```

Simply run `agymod` again to continue with the next account!

## Commands

```bash
# Setup
agymod --add-account-auth <email>   # Add and authenticate account
agymod --auth <index>               # Authenticate existing account
agymod --add-account <email>        # Add account (auth later)

# Usage
agymod                              # Interactive session
agymod <prompt>                     # Single prompt

# Management
agymod --switch <index>             # Switch to specific account (1-based)
agymod --status                     # Show all accounts and current one
agymod --list                       # List configured accounts
agymod --logs                       # View activity log
agymod --reset                      # Reset everything

# Help
agymod --help                       # Show this help
```

## How It Works

1. **Token Storage**: Each account's OAuth token is stored in `~/.agymod/tokens/`
2. **Token Swapping**: When you run `agymod`, it loads the current account's token
3. **Auto-Rotation**: When quota is reached, the next account's token is loaded automatically
4. **Isolation**: Each account remains completely isolated with its own quota

## Config Location

- **Main config**: `~/.agymod/`
- **Accounts file**: `~/.agymod/accounts.json`
- **OAuth tokens**: `~/.agymod/tokens/`
- **Activity log**: `~/.agymod/agymod.log`

## Example Workflow

```bash
# Setup 3 accounts
$ agymod --add-account-auth yakisec@gmail.com
✓ Account added: yakisec@gmail.com
Authenticating: yakisec@gmail.com
[agy opens for OAuth login...]
✓ Token saved for: yakisec@gmail.com

$ agymod --add-account-auth kirucianaz@gmail.com
✓ Account added: kirucianaz@gmail.com
Authenticating: kirucianaz@gmail.com
[agy opens for OAuth login...]
✓ Token saved for: kirucianaz@gmail.com

$ agymod --add-account-auth groksec@gmail.com
✓ Account added: groksec@gmail.com
Authenticating: groksec@gmail.com
[agy opens for OAuth login...]
✓ Token saved for: groksec@gmail.com

# Check setup
$ agymod --status
═══════════════════════════════════════════════════════════
  agymod Status
═══════════════════════════════════════════════════════════

Total accounts: 3
Current account: 1
Total rotations: 0

=== Configured Accounts ===

  → 1. [✓] yakisec@gmail.com
    2. [✓] kirucianaz@gmail.com
    3. [✓] groksec@gmail.com

Current: Account 1
Rotations: 0
═══════════════════════════════════════════════════════════

# Use it
$ agymod
[agymod] Using account: yakisec@gmail.com (1/3)
> solve this ctf challenge
[response...]

Did you hit quota? (y/n)
> y

⚠ QUOTA REACHED - AUTO-ROTATED
Previous account: yakisec@gmail.com
New account: kirucianaz@gmail.com

To continue:
  agymod

# Continue seamlessly
$ agymod
[agymod] Using account: kirucianaz@gmail.com (2/3)
> continue with the challenge
[response...]
```

## Requirements

- **agy** (Antigravity CLI) - installed and in PATH
- **bash** 4.0+
- **jq** - for JSON parsing

Install dependencies:
```bash
# macOS
brew install jq

# Ubuntu/Debian
sudo apt-get install jq

# Fedora
sudo dnf install jq
```

## Security

- OAuth tokens are stored locally in `~/.agymod/tokens/`
- Tokens are only loaded when `agymod` is run
- Each account is completely isolated
- No tokens are logged or exposed

**Keep `~/.agymod/` private!** Don't commit it to git.

## Troubleshooting

**Issue**: "agy not found"
```bash
# Make sure agy is installed and in PATH
which agy
```

**Issue**: "Token file not found"
```bash
# Re-authenticate the account
agymod --auth 0  # 0-based index
```

**Issue**: "All accounts exhausted"
```bash
# Check quota reset time in agy output
# Quotas reset every ~1.5 hours per account
# Or add more accounts and authenticate them
agymod --add-account-auth another-account@gmail.com
```

## License

MIT

## Contributing

Pull requests welcome!

---

Built for endless HackTheBox sessions 🎯
