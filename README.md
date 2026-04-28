# ai-driven-newsletter

**Read it here:** [https://mpallone.github.io/ai-driven-newsletter/](https://mpallone.github.io/ai-driven-newsletter/)

Daily AI-tools digest, published as a static HTML page.

The skill that generates the digest lives at
[`.claude/skills/daily-ai-tools-digest/SKILL.md`](.claude/skills/daily-ai-tools-digest/SKILL.md).
A Claude Routine runs it daily; each run archives the prior `index.html`
under `archive/` and writes a fresh page to `index.html`.