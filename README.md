# 🛡️ Bulletproof

**Make your AI code bulletproof.**

> 75% of AI agents break previously working code. Bulletproof makes sure yours doesn't.

An agent skill that embeds verification loops into every stage of development — so you ship code that actually works, not code that looks like it works.

**Author:** Artemiy Miller · [Telegram](https://t.me/artemiimillier) · [GitHub](https://github.com/artemiimillier) · [Email](mailto:who.ismillerr@gmail.com)

> Suggestions, bugs, ideas? Open an [issue](https://github.com/artemiimillier/bulletproof/issues) or email **who.ismillerr@gmail.com**

---

## What It Does

Bulletproof is a development workflow for AI coding agents. Instead of letting the AI write code and hope for the best, it forces every change through a gauntlet of checks:

- **Challenge Loop** — Before writing code: "Is this actually the best solution? Is there code for code's sake?"
- **False-Positive Bug Filter** — Find bugs → prove they're real → only then fix. No cosmetic changes.
- **Impact Analysis** — Before merging: "Did we break anything else? What happens in a month?"
- **Anti-Rationalization Hook** — Catches the AI saying "out of scope" or "pre-existing issue" when work is incomplete.
- **Adaptive Sizing** — A bug fix gets a lightweight check. A new service gets the full 12-stage pipeline.

Works with **Claude Code, Codex, Gemini CLI, Cursor, Windsurf, OpenCode** — any tool supporting the Agent Skills standard.

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
├── README.md
├── CHANGELOG.md
└── LICENSE               # MIT
```

---

## Methodology

Built on research from: HumanLayer (context management), Trail of Bits (anti-rationalization hooks), Addy Osmani (spec-first workflow), GitHub Spec Kit (spec-driven development), SWE-CI Benchmark (75% regression data), TDAD/arXiv (impact analysis), Anthropic Code Review (false-positive filtering), Spotify Engineering (verification loops), RIPER-5 (phase separation), Boris Tane (annotation cycle).

---

## License

MIT — use it, modify it, share it. 100% original work. All sources credited.

*Built by [Artemiy Miller](https://github.com/artemiimillier) · v5.0 · [who.ismillerr@gmail.com](mailto:who.ismillerr@gmail.com)*
