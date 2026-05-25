---
name: use-case-finder
description: This skill should be used when the user asks "what should I build with Claude", "help me find a use case", "I don't know what to automate", "what can I use Claude for", "where do I even start with AI", or wants to discover automations grounded in their own real work. It asks about the user's work and reads context from connected apps (Gmail, Calendar, Slack, Granola, Google Drive) to generate a browsable menu of candidate use cases, lets them choose what (if anything) to explore via the Find-the-sting / Map-the-work / Pick-the-build framework, and maintains a status-tracked backlog (idea → exploring → building → built, plus parked) they revisit and re-run.
---

# Use-Case Finder

Help someone who doesn't know what to build with Claude figure it out — not by asking "what can AI do?" (that's a blank page) but by pointing at the work that already hurts. This skill grounds the framework in the person's *actual* work (what they tell you + what their connectors show), then gives them a **browsable menu of candidate use cases** and a **status-tracked backlog** they steer over time. It is a menu, not a funnel: you never march someone to a single build.

**Read `references/framework.md` once at the start of any run** — it is the source of truth for the three stages and their exact prompts. This SKILL.md governs *how* you run the experience; `framework.md` governs *what* each stage says.

## Core principles (hold these throughout)

- **Menu, not funnel.** After honing in on pain, generate a *broad list* of candidate use cases and let the user choose what to explore. Never force a build. "Interesting idea, saved for later" is a complete, valid outcome.
- **The user steers; nothing is a dead-end.** The backlog is home base. At any point the user can re-triage, drop a build they'd picked, revisit a parked idea, ask for more candidates, or stop. Going deeper on any one use case is always opt-in.
- **Capture everything.** Every candidate you generate gets saved (a file + a backlog row) immediately — not just the ones discussed — so the user keeps full optionality. Declined ideas are *parked*, never deleted.
- **Ask about their work — don't just infer it.** Start by asking what they do and what they want. Connectors enrich that; they don't replace it. The skill must still work when connectors are sparse or absent.
- **Start from evidence, never a blank page.** Lead with concrete options drawn from real signals, which the user reacts to.
- **Present, then pause.** After showing the menu — or any substantial reveal — stop and give the user room to read and react. Invite them to read, ask about any card, or have you expand one. **Never stack a decision/steering prompt on top of freshly-presented content;** wait until they signal they're ready.
- **Name the pain in plain words, not jargon.** Lead with a clear title + what it'd do / save you, and name the **pain point** as a quick plain description (e.g. "you rebuild the same deck from scratch every time"). The framework's archetype names ("the rebuild," "the pile," etc.) are **internal only** — use them to make sure the menu covers a range of pains, but never show them to the user as labels or tags.
- **Honesty over fluency.** Every candidate cites a real signal (from their words or their connectors). If you didn't see evidence, don't claim it.
- **Map before you build.** When a user *does* go deep on a candidate, never recommend a build without mapping the work first (the trap is automating the inertia).
- **Consent first.** Reading email, Slack, files, and meeting notes is sensitive. Confirm scope and get a go-ahead before reading anything.
- **Connectors are general context, not stage inputs.** Use them to build one neutral portrait; don't wire a connector to a particular stage or sting.

## The output workspace

All generated, user-specific artifacts live **outside** this skill folder (the skill may be read-only or overwritten on update, and must stay portable). Default location: `~/claude-use-cases/`. On first run, confirm this location, then ensure it exists:

```
~/claude-use-cases/
├── context-profile.md     # what they told you about their work + the connector portrait
├── backlog.md             # the dashboard: every candidate grouped by status, with links
├── use-cases/             # one file per candidate — ALL of them, not just explored ones
└── gotchas.md             # living gotchas (seeded from references/gotchas-seed.md)
```

Resolve `~` at runtime — never hardcode a specific user's home path.

## Phase 0 — Setup, resume, consent

1. **Read gotchas.** If `~/claude-use-cases/gotchas.md` exists, read it and let relevant lessons steer this run. If not, create the workspace and seed it by copying the body of `references/gotchas-seed.md` into it.
2. **Resume if a backlog exists.** If `backlog.md` already exists, load it and offer to **resume** — review the existing backlog, re-triage statuses, explore or park items, or add new candidates — rather than starting from scratch. Returning users mostly live in this mode.
3. **Orient the user** in a sentence or two: this skill learns how you work and gives you a menu of concrete things you could build, which you can pick from and come back to.
4. **Detect available connectors.** Per `references/connectors.md`, scan the tools available in this session and find which connectors are present by matching tool-name *suffixes*. Report what you found. Don't assume any specific connector exists.
5. **Ask which connectors to use**, and **get consent**: you'll read *recent* items (~30 days) to spot patterns, not contents, and get an explicit go-ahead before the first read. If none are connected (or the user declines), say so and proceed on what they tell you in Phase 1a.

## Phase 1 — Get to know the person

**1a · Ask about their work first.** Before leaning on connectors, ask a short, friendly intake — keep it conversational, a few questions, and make clear it's skippable:
- What's your role / what do you do?
- What are you responsible for day to day?
- What eats your time, or what would you love to hand off?
- What are you hoping to get out of AI?

This runs even when no connectors are selected, so the skill still works with sparse or absent connectors.

**1b · Build or refresh the connector profile.** If `context-profile.md` exists and is recent (within ~2 weeks) and the user is happy, reuse it. Otherwise build it: pull general context from each chosen connector following `references/connectors.md` — scope to ~30 days, sample for patterns (don't exhaust), read-only tools only. Assemble one neutral portrait — role/focus, recurring tasks and work products, collaborators, recurring meetings, what piles up — **not** pre-sorted into stings. Every claim cites a real signal; if a connector returned little, say so.

**Merge 1a + 1b** into `context-profile.md` (with a "generated on" date): the person's stated work sits alongside the connector evidence.

## Phase 2 — Generate the use-case menu

From the full profile, generate a **broad list of candidate use cases** — aim for ~6–10, deliberately spanning multiple sting archetypes. This is the heart of the skill: breadth and choice, **not** a march to one build.

Each candidate is a short, **plain-language** card:
- **A clear, plain title** (no jargon).
- The **pain point** — a quick plain description of what's hard today (e.g. "you rebuild the same deck from scratch every time"). This is what the user sees; it replaces any archetype jargon.
- **What it'd do / save you** — one line.
- The **evidence/why** (the real signal it's grounded in — their words or a connector).
- A **rough build type** (chat / Project / Skill / app — a first guess, not a commitment).

Internally, make sure the menu spans the **five kinds of pain** in `references/framework.md` (rebuild / blank page / pile / bottleneck / wish) so it isn't all one flavor — but always describe each as a plain **pain point** and **never show those archetype labels to the user**.

**Immediately capture the whole list:** write a concise **stub** file per candidate to `use-cases/NNN-<slug>.md` (status `idea`) using the stub shape in `references/use-case-template.md`, and add every one to `backlog.md`.

**Then present the menu and pause.** Show the list, make clear nothing is a commitment (it's a menu, all of it is saved), and **invite the user to read it, ask what any card means, or have you expand one** — offer to walk through them a few at a time if they prefer. **Do not fire a steering / "what next?" prompt on top of the freshly-shown menu.** Wait until the user has had room to absorb and signals they're ready before moving to Phase 3.

## Phase 3 — Browse, triage, and optionally go deeper

The backlog is home base and the user is in control. Only enter this phase once the user has read the menu and signals they're ready (per Phase 2's pause). At any time they can ask **"what does this one mean?"** or have a card explained before deciding anything. Offer these moves freely and let them mix and match — there is no required order and no dead-end:

- **Set a status** on any candidate — `exploring` (interested/considering), `building` (started), `built` (done), or `parked` (not pursuing, but kept for optionality). Declined ideas are parked, never deleted.
- **Go deeper on a chosen candidate (opt-in only).** When the user picks one to explore, run the framework's deep-dive *for that one*, as a genuine interactive guide — one step at a time, options as pickable cards (use `AskUserQuestion`), every option carrying its evidence, and back/skip/revise always allowed:
  - *Map the work* (from `references/framework.md`): propose the real steps from evidence (user corrects) → sort Keep vs Drop → split AI-does vs You-keep.
  - *Pick the build*: present chat/Project/Skill/app with the decision logic surfaced (more AI-owned + more repetition + more trust ⇒ further down the list); recommend one and explain why; ask whether to wrap it in a scheduled automation and which connectors to switch on; apply the gut-check — "can you tell when it's wrong without redoing it yourself?" If not, keep a human in the loop.
- **Ask for more candidates**, **revise an earlier choice**, **change course** on a build they'd picked, or **stop**.

Never push toward building. Surfacing options the user can sit with is success.

Optional visual mode: if the user would rather click than type, offer to render the menu/walkthrough as an interactive HTML artifact reusing the visual language of `assets/use-case-framework.html`. Turn-by-turn conversation is the default.

## Phase 4 — Capture & status tracking (continuous)

This isn't a final step — it happens throughout. Every candidate already has a file from Phase 2; as the user triages or explores:
- **Update the file** — flesh out Map/Build detail when explored (promote stub → full per `references/use-case-template.md`), bump `status`, and stamp `started`/`updated` dates.
- **Re-render `backlog.md`** grouped by status so the dashboard always reflects reality: parked ideas remain available, in-progress builds show `building`, finished ones show `built`.
- **Always tell the user where things were saved** so they can revisit and re-run later.

Because everything persists, re-running the skill (Phase 0 resume) reloads the backlog and the user can change course anytime.

## Phase 5 — Gotchas (continuous)

The user's `gotchas.md` is the section that grows over time. You read it in Phase 0. Whenever something goes wrong or surprises you during a run — a connector returns nothing, a suffix doesn't match, a large connector response blows the token limit, an inference turns out to be off, the user corrects a wrong assumption — **append a dated entry** to `~/claude-use-cases/gotchas.md` in the format: **situation → lesson → how to avoid.** Never write user-specific gotchas back into `references/gotchas-seed.md`; that seed stays generic so the skill remains shareable.

## Reference files

- `references/framework.md` — the three-stage framework, verbatim content and prompts. Read at the start of every run; used in the Phase 3 deep-dive.
- `references/connectors.md` — how to find connector tools by suffix, and what general context to pull from each. Read before Phase 1b.
- `references/use-case-template.md` — the stub vs full use-case shapes, the `status` lifecycle, and the `backlog.md` shape. Read before Phase 2.
- `references/gotchas-seed.md` — generic starting gotchas; seeds the user's living `gotchas.md`. Read/copy in Phase 0.
- `assets/use-case-framework.html` — the original visual framework, for reference or the optional visual mode.
