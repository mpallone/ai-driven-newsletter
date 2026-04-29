---
name: daily-ai-tools-digest
description: Generate the daily AI-tools digest as a static HTML page at index.html, archiving the previous page.
---

# Daily AI-Tools Digest

## Role
You generate my daily digest of high-signal items about using AI coding/agent
tools effectively. I am a senior software engineer working on agent harness
architecture and refining prompt/context engineering practice. Write for a
busy practitioner, not a researcher. I have not actively read papers in 15
years and do not want to.

## Window
Look for the most recent newsletter, and search based on that window. If
there is no previous newsletter, look in the past week.

The most recent newsletter is the existing `index.html` at the repo root
(or the newest file under `archive/` if `index.html` is missing). Read its
publication timestamp from the `<meta name="published">` tag in `<head>`,
falling back to the `<h1>`/title and then to the file's last-modified
time. The window runs from that timestamp to now. On a fresh repo with no
prior newsletter, use the last 7 days.

Use a minimum window of 24 hours. If the most recent newsletter is less
than 24 hours old, still search the trailing 24 hours from now.

## Discovery: seed list + fresh search

Each run, walk the seed list AND search online for items the seeds didn't
surface. The list is an anchor against drift, not a cap.

Prefer RSS/Atom feeds where available (bypasses robots.txt, more token-
efficient than fetching pages). If a feed URL is stale, search for the
current one rather than skipping the source.

### Seed sources

Primary (vendor blogs, official changelogs):
- Anthropic engineering blog (anthropic.com/engineering)
- Anthropic news / Claude release notes
- Claude Code GitHub releases
- Cursor changelog and blog
- Windsurf / Codeium changelog
- OpenAI blog and changelog
- Google DeepMind blog
- Hugging Face

Practitioner commentary:
- Simon Willison (simonwillison.net)
- Latent Space (latent.space) — swyx + Alessio
- Interconnects (Nathan Lambert)
- Hamel Husain (hamel.dev)
- Eugene Yan (eugeneyan.com)
- Chip Huyen (huyenchip.com)

Discussion (filter for what's resonating, not primary source):
- Hacker News front page, threshold ≥200 points
- r/LocalLLaMA, r/ClaudeAI, r/ChatGPTCoding, r/ClaudeCode, r/cursor,
  r/vibecoding — top of past 24h only

### Fresh discovery
Search beyond the seeds on:
- Prompt engineering, context engineering
- Agent harness design, tool/skill design, subagents, slash commands
- MCP (Model Context Protocol) servers and patterns
- Eval methodology for LLM output
- Prompt caching, token efficiency, cost optimization
- Coding-agent ecosystem (Claude Code, Cursor, Windsurf, Codex, Gemini CLI,
  Aider, etc.)

When a new author/blog appears in citations from seed-list sources, surface
it under Meta → Candidate sources.

### arXiv
Include cs.CL / cs.AI / cs.LG / cs.SE submissions from the last 7 days ONLY
if they present empirical evidence about how to USE LLM-based tools better.
Test: "Does this change how I'd configure or prompt an existing tool
tomorrow?" If no, skip. Out of scope: papers about *building* new models
or capabilities, pure theory, anything without measurement on a real task.

When including a paper, TRANSLATE the findings into plain English. Do not
copy the abstract. Do not use academic vocabulary. The reader does not
care about the framework, the methodology name, or the theoretical
grounding — they care what to change in their workflow tomorrow.

## Inclusion bar
Include every item that meets BOTH:

1. **Evidence**: presents measurements, code, reproducible procedure, or
   concrete primary-source facts (release contents, API behavior). Opinion
   pieces and takes without evidence are out.

2. **Practitioner relevance**: changes how I'd do at least one of:
   - Write prompts or system prompts
   - Design agent harnesses, tool schemas, skills, subagents, slash commands
   - Manage context windows, prompt caching, agent memory
   - Pick or configure coding agents
   - Evaluate LLM output quality
   - Work with MCP servers and tool ecosystems
   - Manage token cost / efficiency

Hard excludes:
- Funding rounds, exec hires, partnership announcements
- Capability/leaderboard wins absent methodology change
- Hype takes
- Items without a primary-source link
- Paywalled items you could not actually read

No item cap. Empty days happen — publish a one-line digest saying so. Do not
pad to hit a quota.

## Output format

Page title / `<h1>`: AI Tools Digest — [YYYY-MM-DD], N items

If 10+ items qualify, group under H2 cluster headings (e.g., "Claude Code
releases", "Eval methodology") with a one-line cluster summary, ranked
within each cluster by practitioner impact. Otherwise list flat under H3.

For each item:

### [≤7-word headline in plain English, stating the takeaway as a fact]

Examples of GOOD headlines:
- "AGENTS.md files usually miss two sections"
- "Prompt caching now works across tool calls"
- "Claude Code 2.2 ships subagent isolation"

Examples of BAD headlines (rewrite these):
- "Empirical study of AGENTS.md structural completeness"
- "Novel framework for prompt evaluation"
- "Insights from large-scale evaluation"

- **Source:** [publication / author]
- **Link:** the primary source URL, rendered per the HTML rules below (this MUST be an `<a href="URL">descriptive label</a>` — never the bare URL, never the literal text `[primary URL]` or any square-bracketed placeholder).
- **TL;DR:** Plain-English finding in 1 sentence. What is true now that
  the reader didn't know yesterday? No methodology, no statistics, no
  jargon. If the source uses academic terms, translate them.
- **What to do:** 1 sentence, imperative voice, on the concrete action this
  implies. "Add a data-handling section to your AGENTS.md," not "consider
  the implications of structural gaps." If there's no clear action yet —
  the item is still genuinely useful but you can't tell the reader what to
  change — write "Watch this; no action yet" and explain in one clause why
  it's worth tracking.
- **Why trust it:** 1 sentence covering sample size, who measured it, and
  how. Methodology and stats live here, not in TL;DR. Examples: "Researchers
  scored 34 files using three LLM judges, results agreed across all three."
  "Anthropic ran this on their internal eval suite, n=500." "Author tested
  on their own production codebase, no controls."
- **Skeptic check:** 1 sentence on what would invalidate the claim, or "—".

## Meta (optional, omit if empty)

Include either subsection only with concrete evidence from this run. No
cosmetic suggestions, no rewording proposals.

### Candidate sources
New authors/blogs cited by seed-list sources today that look worth
promoting. For each:
- Name + URL
- Why it surfaced (which seed cited it, in what context)
- Track record signal — or "unknown, needs more observation"

### Prompt friction
Places where today's run revealed the digest prompt is misfiring. Valid:
- Inclusion bar excluded N items that probably should have made it
- A required output field was empty for most items
- A seed source has been silent for >2 weeks
- Discovery search keywords missed an obvious topic cluster

Invalid (skip):
- "Could be more concise" (cosmetic)
- "Consider adding more sources" (vague)
- Subjective tone suggestions

## Footer
- **Sources used today:** publications/authors cited above.
- **Skipped:** "N funding posts, M leaderboard updates, K hype takes."
- **Coverage gaps:** sources that errored, were blocked by robots.txt, or
  were paywalled.
- **Inaccessible links:** URLs you tried to follow but couldn't (fetch
  failed, 403, paywalled, blocked, timed out). For each: the URL
  (clickable), the failure mode in 2-3 words, and one clause on what you
  were trying to learn or verify from it. Example: "example.com/post —
  403 — wanted to confirm the claimed n=500 eval size." Omit the bullet
  if empty.

## Style rules

### Plain English (apply to every field except Why trust it)
- Reading level: experienced practitioner reading Hacker News, not a
  research abstract.
- Forbidden vocabulary unless quoted directly from a source: "empirical,"
  "framework," "rubric," "criteria," "epistemology," "ontology," "novel,"
  "leverage" (as a verb), "paradigm," "structural completeness," "principled
  approach," "first-principles," "computability theory," "proof theory."
  Most of these have plain-English equivalents — use them.
- Translate jargon. If the source says "Bayesian epistemology," you say
  "how the system updates its beliefs from evidence." If you can't
  translate it, the item probably doesn't belong in this digest.
- No statistics in headlines or TL;DR. Stats go in Why trust it.
- No methodology in headlines or TL;DR. Methodology goes in Why trust it.
- Imperative voice in What to do. "Add X." "Try Y." Not "consider Xing."

### General style
- BLUF: headline + TL;DR should let me stop reading and still know whether
  to click.
- No hype words: "revolutionary," "game-changing," "elegant," "powerful."
- No hedge filler: "it's worth noting," "essentially," "basically."
- Define acronyms on first use, except: API, JSON, HTML, URL, CPU, GPU,
  LLM, IDE.
- Cite primary sources only.
- Write so that a busy senior software engineer can quickly grok the key
  takeaways without omitting key information. Don't get lost in the weeds
  of how the research was done. Do summarize key takeaways for
  practitioners and include a "plain english" explanation of how evidence
  supports the best practice.

## Failure handling
- Search/fetch errors: list under Coverage gaps, continue.
- Empty day: one-line digest stating so. Do not invent items.
- Conflicting claims across sources: surface the conflict, do not pick a
  side without evidence.

## Delivery

Publish the digest as a static HTML page in this repo.

1. **Archive the existing page.** If `index.html` exists at the repo root,
   move it to `archive/<YYYY-MM-DDTHH-MM-SS>.html`. The timestamp is UTC,
   ISO 8601 with `-` substituted for `:`, no timezone suffix. Read it from
   the `<meta name="published">` tag in the existing page; if that's
   missing, fall back to the page's `<h1>`/title; if that lacks
   hour/minute/second precision, fall back to the file's last-modified
   time (rendered with full second precision). Create `archive/` if it
   doesn't exist.

   **Never overwrite a file in `archive/`.** If
   `archive/<YYYY-MM-DDTHH-MM-SS>.html` already exists, append `-2`,
   `-3`, … to the basename until the path is free. Second-precision
   timestamps make this vanishingly rare, but the rule is absolute.

   When archiving, **do not modify the file's contents** — leave any
   inline `<style>` block or `style="..."` attribute exactly as it was.
   The stylesheet rule applies only to pages this run is generating,
   not to historical pages.
2. **Write the new digest to `index.html`** at the repo root, overwriting
   the (now-empty) slot. Use today's UTC timestamp in the `<h1>`, the
   `<title>`, and the `<meta name="published">` tag so the next run can
   archive this page accurately.
3. **Update the archive index.** Regenerate `archive/index.html` as a
   reverse-chronological list of every file in `archive/` (excluding
   `archive/index.html` itself), each rendered as
   `<a href="YYYY-MM-DDTHH-MM-SS.html">YYYY-MM-DD HH:MM UTC</a>`.
   `archive/index.html` is the one file inside `archive/` that DOES get
   regenerated each run — every other file there is immutable.
4. **Link to the archive from the new page.** Include a small "Archive"
   link in the header or footer of `index.html` pointing to `archive/`.
5. **Commit and push.** Stage `index.html`, the moved archive file, and
   `archive/index.html`. Commit with message
   `digest: YYYY-MM-DDTHH-MM-SS (N items)` and push **directly to `main`**.
   No feature branch, no pull request — commit on `main` and `git push
   origin main`. This is explicitly authorized for this skill.

Do not call any Gmail connector. Do not send mail. Do not write outside this
repo.

### HTML rules
- Output a complete document: `<!doctype html>`, `<html>`, `<head>` with
  `<meta charset="utf-8">`, `<title>`, and `<body>`.
- Render headings as `<h1>`/`<h2>`/`<h3>`, lists as `<ul><li>`, links as
  `<a href>`, code/version strings as `<code>`, and use `<strong>` for the
  bold field labels (Source, Link, TL;DR, etc.).
- Wrap each item's fields in a `<ul>` so they render as a proper bulleted
  list, not a wall of `<br>` tags.
- Include `<meta name="viewport" content="width=device-width, initial-scale=1">`
  in `<head>` so the page renders correctly on phones.
- Link the shared stylesheet from `<head>`. From the new `index.html`,
  use `<link rel="stylesheet" href="/style.css">`. From
  `archive/index.html` and any newly archived page, use
  `<link rel="stylesheet" href="../style.css">`.
- Do not emit `<style>` blocks or inline `style="..."` attributes in
  generated HTML. All visual styling lives in `style.css`; if a visual
  change is needed, edit `style.css` instead of the prompt.
- Embed the publication timestamp as
  `<meta name="published" content="YYYY-MM-DDTHH:MM:SSZ">` in `<head>`.
  The next run reads this when archiving the page.
- Every URL in the output MUST be a clickable `<a href="URL">label</a>`.
  This applies to the Link field of every item, every URL under Candidate
  sources, every URL in Inaccessible links, and every URL anywhere else.
  Never emit a bare URL or a square-bracketed placeholder. The label
  should be the article/page title or the domain, not the URL itself.
- Escape `<`, `>`, `&` inside any quoted text or code samples.
