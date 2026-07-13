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

### Quick Install (One-liner)

```bash
curl -fsSL https://raw.githubusercontent.com/zahidoverflow/agymod/main/agymod -o agymod && chmod +x agymod && sudo mv agymod /usr/local/bin/
```

Or with sudo for direct installation:

```bash
sudo bash -c 'curl -fsSL https://raw.githubusercontent.com/zahidoverflow/agymod/main/agymod -o /usr/local/bin/agymod && chmod +x /usr/local/bin/agymod'
```

### Manual Installation

```bash
# Clone the repository
git clone https://github.com/zahidoverflow/agymod.git
cd agymod

# Make executable
chmod +x agymod

# Install to PATH
sudo cp agymod /usr/local/bin/
```

### Verify Installation

```bash
agymod --help
```

## Quick Start

### Setup (One command per account)
```bash
agymod --add-account-auth your-account-1@gmail.com
agymod --add-account-auth your-account-2@gmail.com
agymod --add-account-auth your-account-3@gmail.com
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
[agymod] Using account: your-account-1@gmail.com (1/3)
> hello

Did you hit quota? (y/n)
> y

⚠ QUOTA REACHED - AUTO-ROTATED
Previous account: your-account-1@gmail.com
New account: your-account-2@gmail.com

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
$ agymod --add-account-auth your-account-1@gmail.com
✓ Account added: your-account-1@gmail.com
Authenticating: your-account-1@gmail.com
[agy opens for OAuth login...]
✓ Token saved for: your-account-1@gmail.com

$ agymod --add-account-auth your-account-2@gmail.com
✓ Account added: your-account-2@gmail.com
Authenticating: your-account-2@gmail.com
[agy opens for OAuth login...]
✓ Token saved for: your-account-2@gmail.com

$ agymod --add-account-auth your-account-3@gmail.com
✓ Account added: your-account-3@gmail.com
Authenticating: your-account-3@gmail.com
[agy opens for OAuth login...]
✓ Token saved for: your-account-3@gmail.com

# Check setup
$ agymod --status
═══════════════════════════════════════════════════════════
  agymod Status
═══════════════════════════════════════════════════════════

Total accounts: 3
Current account: 1
Total rotations: 0

=== Configured Accounts ===

  → 1. [✓] your-account-1@gmail.com
    2. [✓] your-account-2@gmail.com
    3. [✓] your-account-3@gmail.com

Current: Account 1
Rotations: 0
═══════════════════════════════════════════════════════════

# Use it
$ agymod
[agymod] Using account: your-account-1@gmail.com (1/3)
> solve this ctf challenge
[response...]

Did you hit quota? (y/n)
> y

⚠ QUOTA REACHED - AUTO-ROTATED
Previous account: your-account-1@gmail.com
New account: your-account-2@gmail.com

To continue:
  agymod

# Continue seamlessly
$ agymod
[agymod] Using account: your-account-2@gmail.com (2/3)
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

## Open Source & Community

**agymod is fully open source.** You're free to:

✅ **Use it** - Clone, install, and use in any project (personal or commercial)  
✅ **Modify it** - Fork and customize to your needs  
✅ **Build on it** - Create derivatives, improvements, or extensions  
✅ **Share it** - Help others by sharing your modifications back  

### Build Your Own

The entire source code is available in this repository. If you want to:
- Add new features
- Integrate with other CLI tools
- Create variants for other AI platforms (Claude, OpenAI, etc.)
- Adapt for different use cases

Feel free to fork and build! The MIT license gives you complete freedom.

### Contributing Back

Found improvements? Have a better approach? Pull requests welcome! 

Whether it's bug fixes, performance improvements, or new features, the community benefits when we share back.

### Related Projects

Interested in building similar tools? agymod is designed to be:
- **Simple** - Easy to understand and modify (~200 lines of bash)
- **Modular** - Can be adapted for other CLIs
- **Extensible** - Base for building similar quota managers

Use agymod as a reference or starting point for your own projects!

---

Built for endless HackTheBox sessions 🎯  
Open source • MIT License • Contributions welcome
