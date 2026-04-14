# fact-checker

> 🇰🇷 [한국어 README](./README.ko.md)

**Automated fact-checking engine using triangulation, deductive reasoning, numerical verification, and LLM weakness compensation. Extracts facts from documents, verifies them via web search, and generates correction suggestions.**

## Prerequisites

- **Claude Cowork or Claude Code** environment
- Web search access (for source verification)

## Goal

Documents contain factual claims — revenue figures, dates, ratios, facility specs — that can drift from reality through rounding, unit confusion, or outdated sources. This skill systematically extracts every verifiable fact, cross-checks it against independent sources, and flags discrepancies with ready-to-apply fixes.

## When & How to Use

Say `"팩트체크해줘"` with a file path. The skill runs in two modes: **LIGHT** checks numbers, dates, and quantities only; **DEEP** (default) checks everything including causal claims and missing evidence. After verification, it presents corrections for your approval before applying edits.

## Use Cases

| Scenario | Prompt | What Happens |
|---|---|---|
| Pre-submission proposal review | `"이 제안서 팩트체크해줘"` | DEEP mode: extracts all facts via 5W1H, verifies with 15+ searches, reports with fix suggestions |
| Quick number check | `"라이트 팩트체크 — 숫자만"` | LIGHT mode: When + Where + How much only, fast pass |
| IR material prep | `"IR 자료 수치 검증해줘"` | Strict tolerance (decimal precision), Python arithmetic on every ratio |

## Key Features

- **5W1H Extraction** — Facts categorized by Who/What/When/Where/How much/Why for zero-miss coverage
- **Source Grading (S1–S4)** — Official filings > trade press > general media > wikis. No "multiple sources agree" without grade
- **Python Arithmetic** — Every ratio verified by division, not eyeballed. Catches 97.94% vs 98.26% differences
- **LLM Weakness Compensation** — Two-pass scanning for parenthetical numbers, table cells, and collapsed content that LLMs skip
- **Tolerance by Purpose** — IR docs need decimal precision; proposals allow rounding. Context-aware grading
## Works With

- **[research-frame](https://github.com/jasonnamii/research-frame)** — Deep research when fact-checking surfaces knowledge gaps
- **[trigger-dictionary](https://github.com/jasonnamii/trigger-dictionary)** — Pre-mortem thinking for missing evidence detection

## Installation

```bash
git clone https://github.com/jasonnamii/fact-checker.git ~/.claude/skills/fact-checker
```

## Update

```bash
cd ~/.claude/skills/fact-checker && git pull
```

Skills placed in `~/.claude/skills/` are automatically available in Claude Code and Cowork sessions.

## Part of Cowork Skills

This is one of 25+ custom skills. See the full catalog: [github.com/jasonnamii/cowork-skills](https://github.com/jasonnamii/cowork-skills)

## License

MIT License — feel free to use, modify, and share.