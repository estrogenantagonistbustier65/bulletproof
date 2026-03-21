# 🛡️ Bulletproof

[![GitHub stars](https://img.shields.io/github/stars/artemiimillier/bulletproof?style=for-the-badge&logo=github)](https://github.com/artemiimillier/bulletproof/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=for-the-badge)](CONTRIBUTING.md)
[![Last Commit](https://img.shields.io/github/last-commit/artemiimillier/bulletproof?style=for-the-badge)](https://github.com/artemiimillier/bulletproof/commits/main)
[![Claude Code](https://img.shields.io/badge/Claude_Code-compatible-blue?style=for-the-badge)](https://claude.com/claude-code)
[![Cursor](https://img.shields.io/badge/Cursor-compatible-blue?style=for-the-badge)](https://cursor.com)

**Make your AI code bulletproof.**

> 75% of AI agents break previously working code. Bulletproof makes sure yours doesn't.

An agent skill that embeds verification loops into every stage of development — so you ship code that actually works, not code that looks like it works.

**Author:** Artemiy Miller · [Telegram](https://t.me/artemiymiller) · [GitHub](https://github.com/artemiimillier) · [Email](mailto:who.ismillerr@gmail.com) · [TG Channel](https://t.me/+0jZamDvGOeZjOWE1)

> Suggestions, bugs, ideas? Open an [issue](https://github.com/artemiimillier/bulletproof/issues) or email **who.ismillerr@gmail.com**
>
> Updates and new versions — join the [Telegram channel](https://t.me/+0jZamDvGOeZjOWE1)

---

## The Problem

You ask an AI agent to fix a bug. It "fixes" it — and breaks three other things. Or it refactors code that didn't need refactoring. Or it says "out of scope" when the work is half-done.

**This is the default behavior of every AI coding agent.** The SWE-CI benchmark (Alibaba, 2025) showed that 75% of AI agents introduce regressions into previously working code.

Bulletproof fixes this.

---

## What It Does

Instead of letting the AI write code and hope for the best, Bulletproof forces every change through a gauntlet of checks:

- **Challenge Loop** — Before writing code: "Is this actually the best solution? Is there code for code's sake?"
- **False-Positive Bug Filter** — Find bugs → prove they're real → only then fix. No cosmetic changes.
- **Impact Analysis** — Before merging: "Did we break anything else? What happens in a month?"
- **Anti-Rationalization Hook** — Catches the AI saying "out of scope" or "pre-existing issue" when work is incomplete.
- **Adaptive Sizing** — A bug fix gets a lightweight check. A new service gets the full 12-stage pipeline.

Works with **Claude Code, Codex, Gemini CLI, Cursor, Windsurf, OpenCode** — any tool supporting the Agent Skills standard.

---

## Before & After

### Without Bulletproof

```
You: "Fix the login timeout bug"
Agent: *changes 12 files, refactors auth module, adds new middleware*
Agent: "Fixed! Also improved the code structure while I was there."
Result: Login works. Password reset is broken. Session handling has a race condition.
```

### With Bulletproof

```
You: "Fix the login timeout bug"
Agent: *researches → plans → implements only what's needed*
Agent: *self-audit: does this match the spec?*
Agent: *verification: are these real bugs or false positives?*
Agent: *impact analysis: did we break password reset? session handling?*
Agent: "Fixed. 2 files changed. All tests pass. No regressions."
Result: Login works. Everything else still works.
```

> See more examples in the [examples/](examples/) folder.

---

## Install (30 seconds)

### Into your project (recommended)

```bash
cd your-project
mkdir -p .claude/skills
git clone https://github.com/artemiimillier/bulletproof.git .claude/skills/bulletproof
```

### Global (works in every project)

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/artemiimillier/bulletproof.git ~/.claude/skills/bulletproof
```

### VS Code with Claude Code extension

Same as above — open the integrated terminal (`Ctrl+``) and run the install command. Claude Code in VS Code reads skills from the same `.claude/skills/` folder.

### For teams (as git submodule)

```bash
git submodule add https://github.com/artemiimillier/bulletproof.git .claude/skills/bulletproof
git commit -m "chore: add bulletproof skill"
```

### Verify it works

Open Claude Code and type `/bulletproof` — it should appear in the skill list. Or just describe a task — Claude invokes Bulletproof automatically when relevant.

---

## How It Works

```
  Size S (bug fix)          Size M (feature)            Size L (architecture)
  ─────────────────       ─────────────────────       ─────────────────────
  1. Research              1. Research                 1. Research
  2. Implement             2. Spec/PRD                 2. Spec/PRD
  3. Self-Audit            3. Plan + Challenge Loop    3. Plan + Challenge Loop
  4. Verify (real bugs?)   4. Implement (TDD)          4. Implement (TDD)
  5. Impact Analysis       5. Self-Audit               5. Self-Audit
  6. Gates                 6. Verify (real bugs?)      6. Verify (real bugs?)
                           7. Impact Analysis          7. Impact Analysis
                           8. Integration Check        8. Integration Check
                           9. Code Review              9. Code Review
                           10. Cleanup                 10. Security Scan
                                                       11. Fixes
                                                       12. Deploy
```

Every stage has a clear purpose. Every check has a reason. Nothing runs "just in case."

---

## Compatible Tools

| Tool | Status |
|------|--------|
| Claude Code | ✅ Native skill support |
| Codex (OpenAI) | ✅ Agent Skills standard |
| Gemini CLI | ✅ Agent Skills standard |
| Cursor | ✅ Agent Skills standard |
| Windsurf | ✅ Agent Skills standard |
| OpenCode | ✅ Agent Skills standard |

---

## Optional: Enable Hooks

Copy the hooks config from `SKILL.md` (Hooks section) into `.claude/settings.json`. This enables automatic branch protection and the anti-rationalization gate.

---

## What's Inside

```
bulletproof/
├── SKILL.md              # The workflow (Claude reads this)
├── templates/
│   ├── research.md       # Research artifact template
│   ├── spec.md           # Specification template
│   ├── plan.md           # Implementation plan template
│   └── handoff.md        # Context handoff template
├── agents/
│   └── code-reviewer.md  # Code review sub-agent
├── examples/             # Before/after use cases
├── CONTRIBUTING.md       # How to contribute
├── README.md
├── CHANGELOG.md
└── LICENSE               # MIT
```

---

## Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Whether it's a bug report, a new example, an improvement to the workflow, or a translation — every contribution helps.

---

## Methodology

Built on research from: HumanLayer (context management), Trail of Bits (anti-rationalization hooks), Addy Osmani (spec-first workflow), GitHub Spec Kit (spec-driven development), SWE-CI Benchmark (75% regression data), TDAD/arXiv (impact analysis), Anthropic Code Review (false-positive filtering), Spotify Engineering (verification loops), RIPER-5 (phase separation), Boris Tane (annotation cycle).

---

## License

MIT — use it, modify it, share it. 100% original work. All sources credited.

*Built by [Artemiy Miller](https://github.com/artemiimillier) · v5.2 · [who.ismillerr@gmail.com](mailto:who.ismillerr@gmail.com) · [Telegram channel](https://t.me/+0jZamDvGOeZjOWE1)*
