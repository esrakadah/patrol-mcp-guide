---
name: progressive-technical-guide
description: Turn a technical topic into a public, beginner-to-advanced guide with verified facts, accurate diagrams, and honest citations. Use when writing or overhauling a README, tutorial, or docs site meant to teach a technology to a mixed-level audience.
---

# Progressive technical guide

A repeatable process for writing technical guides that genuinely work for a beginner
and an expert at the same time, without becoming two documents. Built from a review
of well-regarded developer-advocate tutorial repos (LeanCode's Patrol/Marionette MCP
docs, Patrick Loeber's numbered tutorial series, Majid Hajian's architecture repos)
while rewriting `esrakadah/patrol-mcp-guide`.

## 1. Verify before writing a single word of the "current" state

The single most common failure in technical guides is stating a version number, a
tool name, or an architecture claim that was true when a draft was first written but
has since drifted. Before restructuring or expanding a guide:

- Check the actual current version of every package/tool named, from its real
  registry (pub.dev, npm, PyPI), not from memory or an old draft.
- Confirm every named API/CLI surface still exists under that name (things get
  renamed, split, or deprecated).
- Trace every architectural claim ("X calls Y which returns Z") to a primary source
  (official docs, source code, or a maintainer's own post) — not a secondary
  blog summary of a summary.
- If a fact can't be verified, say so in the guide rather than restating an
  unverified claim confidently. A guide that admits "unclear as of writing" is more
  trustworthy than one that's silently wrong.

## 2. Structure for two readers at once, not two documents

Don't fork into "beginner-guide.md" and "advanced-guide.md" — they drift out of sync
immediately. Instead, structure one document so each reader can find their own path:

- **A "choose your path" section near the top**, tagging each major section with a
  level (🟢 Beginner / 🟡 Intermediate / 🔴 Advanced) and one line on who should
  read it and why.
- **Quick start before theory.** Get the reader running something real in the first
  few minutes; explain the underlying model afterward, once they have a concrete
  experience to hang the explanation on. Theory-first is more precise but loses
  beginners before they have a reason to care.
- **A glossary for jargon introduced early but only explained later** (or never).
  If a beginner has to already know the term to understand its own definition,
  it's not a beginner section yet.
- **Push deep detail sideways, not down.** A single README that tries to be
  exhaustive becomes unscannable. Prefer linking to a focused sub-page over
  growing one section to cover every edge case — unless the guide is genuinely
  short enough that one page still scans well (judge by whether a reader can find
  what they need via headings alone in under 10 seconds).

## 3. Diagram only where a picture beats a paragraph

Add a diagram when the thing being explained is fundamentally about **relationships,
sequence, or a decision** — not as decoration. Good candidates:

- **Architecture** (flowchart): components and how they connect. Use when the
  reader needs to know who talks to whom before anything else makes sense.
- **Sequence** (sequenceDiagram): a multi-step interaction over time, especially
  when the order of calls matters and is non-obvious (e.g., a request/response
  loop, a retry, an async handoff).
- **Decision** (flowchart with decision diamonds): "which option do I need,"
  when the guide would otherwise need a wall of prose to cover the branches.

Do not diagram things a table already communicates better (a feature comparison,
a version matrix) — a mermaid diagram that just restates a table adds noise. When
targeting a Markdown host that renders both light and dark themes (GitHub, GitLab),
avoid hardcoded `style`/`fill` colors on mermaid nodes unless you've checked both
themes; plain default styling with clear labels degrades gracefully everywhere.

## 4. Cite real, currently-alive resources — verify before linking

A "further reading" section is worse than none if any link is dead, abandoned, or
superseded. For every external link:

- Confirm the resource still exists and was updated recently enough to be current
  for a fast-moving ecosystem (check last-commit or last-post date).
  Prefer primary sources (the project's own docs/repo) over third-party summaries.
- Prefer resources with visible, plausible adoption signals (stars, being listed in
  a maintained "awesome-X" list) over unverifiable claims — and say so if you
  can't verify a number precisely (e.g., "~1.4k stars" rather than a false-precise
  figure from a source you couldn't confirm).
- If two tools are easy to confuse (e.g., two similarly-named projects from the
  same maintainer solving adjacent problems), call out the distinction explicitly
  rather than letting the reader discover it's not what they wanted three
  paragraphs in.

## 5. Apply baseline repository hygiene

A guide living in a public repo is judged by the repo, not just the prose:

- `LICENSE` — pick one deliberately (MIT for guides that mix explanatory code
  snippets is a safe, permissive default) rather than leaving it implicit.
- `CONTRIBUTING.md` — even a short one signals the repo welcomes fixes, and sets
  expectations (typo fixes vs. structural changes) so drive-by PRs don't surprise
  the maintainer.
- Repository topics/tags set on the host (GitHub topics) so the repo surfaces in
  the relevant ecosystem searches.
- A one-line, accurate repo description matching what's actually inside — the
  description is often the only thing a search result shows.

## Output checklist

Before calling a guide done, confirm:

- [ ] Every version number and tool/API name checked against a primary source today.
- [ ] A "choose your path" or equivalent wayfinding section exists near the top.
- [ ] At least one diagram exists only where it clarifies a relationship, sequence,
      or decision — not decoratively.
- [ ] Every external link verified alive and reasonably current.
- [ ] LICENSE, CONTRIBUTING.md, and repo topics/description are set.
