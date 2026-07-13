# About agymod

## What is agymod?

**agymod** is a multi-account manager for **Antigravity CLI (agy)** that automatically rotates between multiple Google accounts when quota limits are reached.

Stop manually logging out and logging back in. Stop switching accounts in your browser. agymod handles it all seamlessly.

---

## The Problem

Antigravity CLI (agy) has a **~1.5 hour quota per Google account**. When you're working on:
- Long HackTheBox challenges
- Extended coding sessions
- Deep debugging workflows
- Multi-step system design problems

You inevitably hit the quota wall. Then you have to:
1. ❌ Log out of your current account
2. ❌ Log in to a different account
3. ❌ Manually resume your conversation
4. ❌ Repeat every 90 minutes

**agymod solves this.**

---

## The Solution

With **agymod**, you:

1. ✅ Add multiple Google accounts (one command per account)
2. ✅ Start working normally with `agymod`
3. ✅ When quota is hit, just say `y`
4. ✅ Automatically switches to next account
5. ✅ Continue seamlessly

That's it. No manual switching. No browser OAuth flows. Just uninterrupted work.

---

## How It Works

agymod stores each account's OAuth token separately and **swaps them automatically** when:
- You explicitly hit quota and say yes
- The proxy detects quota error (if enabled)
- You manually switch accounts

Each account remains completely isolated with its own 1.5-hour quota.

---

## Perfect For

- 🎯 **HackTheBox Labs** - Long-running challenges that exceed one quota
- 💻 **Extended Coding Sessions** - Deep work that requires uninterrupted AI assistance
- 🔍 **CTF Competitions** - Time-sensitive challenges where quota limits can cost you
- 📚 **Learning & Research** - Long research sessions where constant interruptions break flow
- 🚀 **Production Debugging** - Marathon debugging sessions without quota interruptions

---

## Quick Start

```bash
# Three one-liners to setup
agymod --add-account-auth account1@gmail.com
agymod --add-account-auth account2@gmail.com
agymod --add-account-auth account3@gmail.com

# Then just use it
agymod

# When quota hits
Did you hit quota? (y/n)
> y
✓ Auto-rotated to next account
```

---

## Key Features

| Feature | Details |
|---------|---------|
| 🔐 **Secure Token Storage** | Each account's OAuth token stored separately in `~/.agymod/` |
| 🔄 **Auto-Rotation** | Automatically switches to next account when quota is reached |
| ⚡ **One-Command Setup** | Add and authenticate accounts in a single command |
| 📊 **Activity Logging** | Track all account switches, rotations, and usage |
| 🎮 **Manual Control** | Switch accounts manually anytime with `--switch` |
| 🛡️ **Isolated Accounts** | Each account completely independent with own quota |

---

## Under the Hood

agymod works by:
1. Storing each Antigravity OAuth token in isolation
2. Swapping the active token when you run `agymod`
3. Detecting quota errors and rotating accounts automatically
4. Maintaining detailed activity logs

It's like CLIProxyAPI, but specifically built for agy with a focus on simplicity and reliability.

---

## Requirements

- **agy** (Antigravity CLI) - [Install here](https://antigravity.google/)
- **bash** 4.0+
- **jq** - for JSON parsing

---

## Use Cases

### Case 1: HackTheBox Challenge (3+ hours)
```
Hour 0-1.5: Account 1 (yakisec@gmail.com) - initial exploration
Hour 1.5: Hit quota → Auto-rotate
Hour 1.5-3: Account 2 (kirucianaz@gmail.com) - deep work
Hour 3: Hit quota → Auto-rotate  
Hour 3-4.5: Account 3 (groksec@gmail.com) - final push
✓ Complete challenge without interruption
```

### Case 2: Debugging Production Issue
```
15:00: Start debugging with Account 1
16:30: Quota hit → agymod rotates
16:31: Continue investigation with Account 2
18:00: Quota hit → agymod rotates
18:01: Resume debugging with Account 3
19:15: Issue resolved ✓
```

### Case 3: Extended Research Session
```
$ agymod
Using account: researcher1@gmail.com (1/5)
> [deep research question]
> [follow-up analysis]
Did you hit quota? (y/n)
> y
✓ Rotated to researcher2@gmail.com
> [continue research]
```

---

## Philosophy

**agymod** is built on the principle that:
- Your workflow should never be interrupted by API quotas
- Account management should be invisible to the user
- Setup should take seconds, not hours
- The tool should stay out of your way

No bloat. No unnecessary features. Just reliable quota rotation.

---

## Privacy & Security

- ✅ OAuth tokens stored **locally only** in `~/.agymod/`
- ✅ Tokens **never sent** to external services
- ✅ Each account **completely isolated**
- ✅ Activity logs stored locally
- ✅ `.gitignore` prevents accidental commits of tokens

**Keep `~/.agymod/` private!** It contains your OAuth credentials.

---

## Contributing

Found a bug? Have a feature idea? Pull requests welcome!

---

## License

MIT - Use freely in personal and commercial projects.

---

## Made With

- **bash** - Core scripting
- **jq** - JSON parsing  
- **agy** - Antigravity CLI integration

---

**agymod** — Endless quota. Endless possibilities. 🚀
