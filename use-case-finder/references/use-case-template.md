# Use-case files, status, and the backlog

Every candidate use case is saved as its own file at `~/claude-use-cases/use-cases/NNN-<slug>.md` (zero-padded sequence + short kebab-case name) — **all of them**, from the moment they're generated, not just the ones explored. A file starts as a concise **stub** and is promoted to the **full** shape only when the user chooses to explore it.

## Status lifecycle

Every file carries a `status`. The lifecycle:

- **`idea`** — generated candidate, not yet triaged. (Default at creation.)
- **`exploring`** — the user is considering it / has mapped it but hasn't committed.
- **`building`** — the user has started building it.
- **`built`** — done / in use.
- **`parked`** — the user chose not to pursue it for now, but it's kept for optionality. Never delete a candidate — park it.

Stamp `created` once, and `started` when status first becomes `building`. Always update `updated` on any change.

## Stub shape (written for every candidate at generation)

```markdown
---
id: NNN
slug: <kebab-case-slug>
title: <short human title>
status: idea
sting: <the rebuild | the blank page | the pile | the bottleneck | the wish>
build: <rough first guess: a chat | a Project | a Skill | an app or tool>
connectors_needed: [<e.g. Gmail, Google Drive>]
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---

# <plain-language title — no jargon>

**Pain point:** (a quick plain description of what's hard today, e.g. "you rebuild the same workshop deck from scratch every time")

**What it'd do / save you:** (one plain line)

**Evidence:** (the real signal this is grounded in — their words or a connector, e.g. "4 'weekly update' email threads in 30 days")
```

The `sting:` frontmatter field is **internal taxonomy only** (to ensure the menu spans a range of pains) — describe the pain in plain words in the body; never surface the archetype name to the user. That's enough to be a useful, revisitable backlog item. Don't write Map/Build detail until the user explores it.

## Full shape (promote the stub when a candidate is explored)

Keep the stub frontmatter (with updated `status`/dates) and the top lines, then append:

```markdown
## The pain underneath
(Time / dread / errors / never-gets-done — what actually hurts, and what would change if it got easier.)

## How it runs today
(The real steps from trigger to done, and where it stalls or drains. A short numbered list.)

## The map
**Keep (must stay true):**
- ...
**Drop (only habit):**
- ...
**AI should do:**
- ...
**You keep:**
- ...

## The build
**Recommended:** <build type> — <where to make it>
**Why:** (the decision logic: how much is AI's, how much it repeats, how much you trust it)
**Schedule:** <none | the cadence, e.g. "every Friday 4pm">
**Connectors to switch on:** <list, or "none">

## Next step
(The single most concrete thing to do next. One sentence.)

## Notes / log
(Running notes as the user tries/builds it. Append over time.)
```

## The backlog dashboard

Maintain `~/claude-use-cases/backlog.md` as the home base — every candidate, **grouped by status** so parked ideas and in-progress builds are all visible at a glance. Lead each row with the **plain-language title**, and use a **`Pain point`** column with a quick plain description of what's hard — never the archetype label. Suggested shape:

```markdown
# My Claude use-case backlog

_Last updated: <YYYY-MM-DD> · profile: context-profile.md (generated <date>)_

## 🔨 Building
| # | Use case | Pain point | Build | Started | File |
|---|----------|-----------|-------|---------|------|
| 4 | <title> | <quick plain "what's hard today"> | a Skill (scheduled) | <date> | [open](use-cases/004-<slug>.md) |

## 🔎 Exploring
| # | Use case | Pain point | Build | File |
|---|----------|-----------|-------|------|
| 2 | <title> | <quick plain "what's hard today"> | a Project | [open](use-cases/002-<slug>.md) |

## 💡 Ideas
| # | Use case | Pain point | Rough build | File |
|---|----------|-----------|-------------|------|
| 1 | <title> | <quick plain "what's hard today"> | a Skill | [open](use-cases/001-<slug>.md) |

## ✅ Built
| # | Use case | Pain point | Build | File |
|---|----------|-----------|-------|------|

## 🅿️ Parked (kept for later)
| # | Use case | Pain point | Why parked | File |
|---|----------|-----------|------------|------|
| 5 | <title> | <quick plain "what's hard today"> | not a priority now | [open](use-cases/005-<slug>.md) |
```

Re-render this whenever a status changes. Empty sections can be omitted or left with a header so the user sees the full lifecycle. The backlog reloads on every run (Phase 0 resume), so the user can revisit and change course anytime.
