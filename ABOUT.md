# About agymod

## What is agymod?

**agymod** is a multi-account manager and proxy for **Antigravity CLI (`agy`)** that automatically rotates between multiple Google accounts when quota limits are reached.

Stop manually logging out and logging back in. Stop dealing with desktop keyring conflicts or browser OAuth loops. `agymod` handles multi-account isolation and rotation seamlessly.

---

## The Problem

Antigravity CLI (`agy`) enforces a **5-hour rolling quota and weekly quota per Google account**. When you're working on:
- Long HackTheBox challenges
- Extended coding & security auditing sessions
- Deep debugging workflows
- Multi-step system design problems

You inevitably hit the quota wall. Without `agymod`, you have to:
1. ❌ Log out of your current account
2. ❌ Log in to a different account in the browser
3. ❌ Deal with OS Keyring overwriting your active session
4. ❌ Repeat whenever an account's 5-hour or weekly quota is exhausted

**agymod solves this.**

---

## The Solution

With **agymod**, you:

1. ✅ Add multiple Google accounts (`agymod --add-account-auth email@gmail.com`)
2. ✅ Select or add accounts anytime via the interactive menu (`agymod --accounts`)
3. ✅ Work normally with `agymod`
4. ✅ When quota is hit, press `Enter` (or `y`) at `Did you hit quota? (Y/n)`
5. ✅ Automatically rotates and launches the next verified account immediately

---

## How It Works

`agymod` stores each account's OAuth token separately in `~/.agymod/tokens/` and **swaps them authoritatively** when:
- You confirm quota exhaustion (`Did you hit quota? (Y/n)`)
- You select an account from `agymod --accounts`
- You switch via index (`agymod --switch <n>`) or email (`agymod --email@gmail.com`)

Each token is verified against its expected account email (`.id_token_email` / JWT `.id_token` claim) and isolated from OS Keyring cross-contamination.

---

## Perfect For

- 🎯 **HackTheBox & Penetration Testing** - Long-running assessments that exceed a single account's quota
- 💻 **Extended Coding Sessions** - Deep work that requires uninterrupted AI assistance
- 🔍 **CTF Competitions** - Time-sensitive challenges where quota limits can cost points
- 📚 **Security Research** - Continuous vulnerability research without interruption
- 🚀 **Production Debugging** - Marathon debugging sessions without quota walls

---

## Quick Start

```bash
# Add and authenticate accounts
agymod --add-account-auth account1@gmail.com
agymod --add-account-auth account2@gmail.com
agymod --add-account-auth account3@gmail.com

# Launch interactive selector or start working directly
agymod --accounts
agymod

# Remove expired accounts anytime (auto-reindexes remaining tokens)
agymod --remove-account old-account@gmail.com
```

---

## Key Features

| Feature | Details |
|---------|---------|
| 🔐 **Secure Isolated Storage** | Each account's OAuth token is stored in `~/.agymod/tokens/` with `0600` permissions |
| 🛡️ **Token Identity Verification** | Verifies `id_token_email` and JWT `id_token` claims to prevent account mismatches |
| 🧭 **Interactive Account Selector** | Clean numbered menu (`agymod --accounts`) to switch or add accounts |
| 🔄 **Instant Auto-Rotation** | Rotates to the next ready account and re-launches `agy` automatically |
| 🧹 **Clean Account Removal** | `agymod --remove-account <email\|idx>` deletes the token and re-indexes remaining accounts |
| ⚡ **Userspace Ready** | Runs 100% in userspace (`~/.local/bin`) without requiring `sudo` or `su` |

---

## Requirements

- **agy** (Antigravity CLI) - [Install here](https://antigravity.google/)
- **bash** 4.0+
- **jq** - JSON processor (auto-bootstrapped to `~/.local/bin/jq` if missing)

---

## Use Cases

### Case 1: Extended Security Assessment
```
Session 1: Account 1 (your-account-1@gmail.com) - initial recon & analysis
Quota hit → Press Enter → Auto-rotates & launches Account 2
Session 2: Account 2 (your-account-2@gmail.com) - deep exploitation & PoC
Quota hit → Press Enter → Auto-rotates & launches Account 3
Session 3: Account 3 (your-account-3@gmail.com) - final verification & report
✓ Complete engagement without interruption
```

### Case 2: Interactive Account Selection
```
$ agymod --accounts
Select account (1-12, default [1]) or 0 to add new: 2
[->] Using account: your-account-2@gmail.com (2/12)
```

---

## Privacy & Security

- ✅ OAuth tokens stored **locally only** in `~/.agymod/` (`0700` directory, `0600` files)
- ✅ Tokens **never sent** to external services or exposed in process arguments
- ✅ Parameterized `jq` handling and strict email validation
- ✅ `.gitignore` prevents accidental commits of tokens, state, or logs

**Keep `~/.agymod/` private!** It contains your OAuth credentials.

---

## License

MIT - Use freely in personal and commercial projects.

---

**agymod** — Endless quota. Endless possibilities. 🚀
