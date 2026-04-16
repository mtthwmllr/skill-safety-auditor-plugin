# Skill Safety Auditor Plugin for Claude

A security auditing plugin for Claude Code that reviews Claude Code skills for risks before or after installation.

## Installation

### For Claude Code (Marketplace Plugin)

**Via CLI:**
```bash
claude plugin marketplace add mtthwmllr/my-plugin
claude plugin install skill-safety-auditor@skill-safety-auditor
```

**Or manually via config file:**
```json
{
  "plugins": [
    {
      "name": "skill-safety-auditor",
      "source": {
        "source": "github",
        "repo": "mtthwmllr/my-plugin",
        "path": "plugins/skill-safety-auditor"
      }
    }
  ]
}
```

## Features

### Skills

#### `skill-safety-auditor:skill-safety-auditor` — Skill Safety Auditor

Audits a Claude Code skill for security risks with three flexible modes.

**What it does:**
- Fetches and reviews skills before you download them (Mode 1)
- Reviews a downloaded `.skill` file before installation (Mode 2)
- Audits an already-installed skill from your local directory (Mode 3)
- Checks for credential theft, prompt injection, obfuscation, and more
- Produces a structured report with CRITICAL / WARNING / INFO severity ratings
- Guides you interactively through clearing each warning

**Trigger phrases:**
- "Is this skill safe?"
- "Audit this skill before I install it"
- "Can you check this?" + any skill URL or install command
- Proactively offered whenever you mention installing a skill

**Checks performed:**

| Check | Severity | What it catches |
|---|---|---|
| A1 — Bash / Shell Access | 🟡 WARNING | Shell command execution |
| A2 — Write / Edit Access | 🟡 WARNING | File write capabilities |
| A3 — No allowed-tools | 🟡 WARNING | Undefined tool scope |
| A4 — Overly Broad Tools | 🟡 WARNING | 5+ tools requested |
| B1 — Credential Access | 🔴 CRITICAL | API keys, tokens, secrets |
| B2 — Network Calls in Scripts | 🔴 / 🟡 | Outbound HTTP from scripts |
| B3 — Obfuscated Content | 🔴 CRITICAL | Encoded/hidden payloads |
| B4 — System Modifications | 🔴 CRITICAL | Persistent shell/cron changes |
| B5 — Out-of-dir File Access | 🟡 WARNING | Access outside working dir |
| B6 — Unverifiable Scripts | 🟡 WARNING | Scripts that couldn't be fetched |
| C1 — Safety Overrides | 🔴 CRITICAL | Prompt injection attacks |
| C2 — Fake Permissions | 🔴 CRITICAL | False Anthropic/admin claims |
| C3 — Concealment Instructions | 🔴 CRITICAL | Instructions to hide actions |
| C4 — Instruction Density | 🟡 WARNING | Off-topic instruction overload |
| D1 — Anonymous Source | 🟡 WARNING | No maintainer history |
| D2 — New Repository | 🟡 WARNING | Repo < 30 days old |
| D3 — Description Mismatch | 🟡 WARNING | Content doesn't match purpose |
| D4 — Invalid Frontmatter | 🟡 WARNING | Missing/malformed YAML header |

## License

MIT
