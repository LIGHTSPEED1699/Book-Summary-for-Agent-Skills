# Book-Summary-for-Agent-Skills

Chapter-by-chapter distillations of technical books, formatted as **agent skills** — structured Markdown that an AI coding agent (Claude Code, GitHub Copilot CLI, Amp, Hermes, etc.) can load and apply directly while working.

Each book is converted with the [book-to-skill](https://github.com/virgiliojr94/book-to-skill) workflow: full-text extraction (OCR + Docling for scanned PDFs), then chapter distillation into a fixed shape that agents consume reliably.

## Structure

Every book folder follows the same layout:

```
<book-skill>/
├── SKILL.md          # entry point: when to use, spine of the book, how to navigate
├── glossary.md       # notation and key terms decoded
├── patterns.md       # cross-chapter design patterns + diagnosis playbooks
├── cheatsheet.md     # algorithms, formulas, quick tables
└── chapters/         # one file per chapter:
                      #   Core Idea · Frameworks Introduced · Key Concepts
                      #   Mental Models · Anti-patterns · Reference Tables
                      #   Key Takeaways · Connects To
```

## Books in this repo

| Folder | Book | Chapters |
|---|---|---|
| `skogestad-multivariable-control` | Skogestad & Postlethwaite, *Multivariable Feedback Control: Analysis and Design* (1st ed., 1996) | 12 + appendix |
| `astrom-adaptive-control` | Åström & Wittenmark, *Adaptive Control* (1st ed., 1989) | 13 |
| `stengel-optimal-control-estimation` | Stengel, *Optimal Control and Estimation* (McGraw-Hill, 1994) | 6 + epilogue |
| `shinskey-process-control` | Shinskey, *Process Control Systems: Application, Design, and Adjustment* | chapter-by-chapter |

## How to use with an agent

Drop a folder into your agent's skills directory (e.g. `~/.claude/skills/`, `~/.agents/skills/`, or a project-level `.claude/skills/`). The `SKILL.md` frontmatter tells the agent when the skill applies; the chapter files are loaded on demand so they cost context only when relevant.

They're also useful for humans: each chapter file is a dense study summary with the book's own tables and worked numbers preserved.

## Notes & caveats

- These are **study summaries / derivative notes** generated for personal learning and agent augmentation, not replacements for the original books. Equations in scans that OCR'd noisily were reconstructed from prose context against standard published results — verify before relying on a specific formula.
- All book content © its respective authors and publishers. This repo hosts only the derived summaries; takedown requests will be honored promptly.
