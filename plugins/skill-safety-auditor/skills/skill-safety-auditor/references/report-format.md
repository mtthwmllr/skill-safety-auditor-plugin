# Safety Report Format

Use this template for every audit output. Fill in all sections.
Omit sections that have no findings (e.g. if there are no CRITICAL issues, omit that block).

---

## Template

```
═══════════════════════════════════════════════
  SKILL SAFETY AUDIT REPORT
═══════════════════════════════════════════════

Skill:        [name from frontmatter, or URL if unnamed]
Source:       [URL audited]
Audited on:   [date]
Scripts found: [count] ([list filenames or "none"])

───────────────────────────────────────────────
OVERALL VERDICT
───────────────────────────────────────────────

[Choose one and remove the others]

🔴 DO NOT INSTALL — Critical issues found.
🟡 PROCEED WITH CAUTION — Warnings found. Review remedies below.
🟢 APPEARS SAFE — No significant issues detected. (See notes if any.)

───────────────────────────────────────────────
🔴 CRITICAL ISSUES  ([count])
───────────────────────────────────────────────

[For each critical issue:]

[Check ID] — [Check Name]
Found in: [SKILL.md / script filename]
Detail: [Exact excerpt or pattern that triggered this check, quoted]
Why this matters: [1–2 sentences in plain language]
Action: Do not install this skill. [Any additional guidance e.g. report link]

───────────────────────────────────────────────
🟡 WARNINGS  ([count])
───────────────────────────────────────────────

[For each warning:]

[Check ID] — [Check Name]
Found in: [SKILL.md / script filename]
Detail: [Exact excerpt or pattern that triggered this check, quoted]
Why this matters: [1–2 sentences in plain language]
Remedy: [Step-by-step what to check or do before proceeding]

───────────────────────────────────────────────
🟢 INFO / NOTES  ([count])
───────────────────────────────────────────────

[For each info item:]

[Check ID] — [Check Name]
Note: [Brief plain-language note]

───────────────────────────────────────────────
WHAT WAS REVIEWED
───────────────────────────────────────────────

✅ SKILL.md frontmatter (allowed-tools, name, description)
✅ SKILL.md body (instructions, prompt injection patterns)
[✅ / ⚠️ not fetched] scripts/[filename] — [brief note if not fetched]
[repeat for each script]

───────────────────────────────────────────────
WHAT WAS NOT REVIEWED
───────────────────────────────────────────────

[List anything that could not be audited, e.g.:]
- Referenced scripts that returned 404
- Assets/binary files (not auditable via text review)
- Runtime behaviour (this audit is static analysis only)

───────────────────────────────────────────────
REMINDER
───────────────────────────────────────────────

This is a static pre-install review, not a guarantee of safety.
Even a clean audit does not protect against:
- Supply chain attacks (repo contents changed after audit)
- Runtime behaviour not visible in source
- Skills updated after you install them

When in doubt, don't install.
═══════════════════════════════════════════════
```

---

## Verdict Decision Rules

| Condition | Verdict |
|---|---|
| Any 🔴 CRITICAL finding | DO NOT INSTALL |
| One or more 🟡 WARNINGs, no CRITICALs | PROCEED WITH CAUTION |
| Cannot fetch SKILL.md at all | DO NOT INSTALL (unverifiable) |
| No findings at any severity | APPEARS SAFE |

Always remind the user that a clean audit is not a guarantee.
