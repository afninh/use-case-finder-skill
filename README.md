# Use-Case Finder — a Claude skill

A Claude skill for the person who knows AI could help but has no idea *what to build*. Instead of asking "what can AI do?" (a blank page), it points at the work that already hurts: it asks about your work, reads context from your connected apps, and hands you a **browsable menu of concrete use cases** grounded in your real day-to-day — then lets you steer a **status-tracked backlog** you keep coming back to.

It's built around a simple framework: **Find the sting → Map the work → Pick the build.**

## What it does

1. **Asks about your work** — a short intake (your role, what you're responsible for, what you'd love to hand off, what you want from AI). Works even with no connectors.
2. **Reads your connectors for context** (with your consent, scoped to ~30 days) — Gmail, Google Calendar, Slack, Granola, Google Drive — to build one neutral portrait of how you actually work.
3. **Generates a menu of candidate use cases** — ~6–10 spanning a range of pains, each led by a plain-language **pain point** ("you rebuild the same deck from scratch every time") and what it'd save you. No jargon, and **it never funnels you into building** anything.
4. **You steer a backlog** — explore any candidate in depth (map the work → pick the build), mark ones you're `building`, `park` the ones you're not pursuing (kept, never deleted), or ask for more. The backlog persists and reloads every run so you can change course anytime.
5. **Learns over time** — keeps a growing `gotchas.md` of lessons from each run.

Nothing is forced. "Interesting idea, saved for later" is a perfectly good outcome.

## How it's structured

```
use-case-finder/
├── SKILL.md                     # the orchestrator (the flow above)
├── references/
│   ├── framework.md             # the Find-the-sting / Map-the-work / Pick-the-build framework
│   ├── connectors.md            # how to find connector tools + what context to pull
│   ├── use-case-template.md     # the use-case file + backlog shapes, and the status lifecycle
│   └── gotchas-seed.md          # generic starting lessons that seed your living gotchas
└── assets/
    └── use-case-framework.html  # the original visual framework (style reference for the optional visual mode)
```

Your generated, personal artifacts (your profile, use cases, backlog, and gotchas) are written to a separate workspace — **`~/claude-use-cases/`** — never inside the skill folder.

## Install

Copy the `use-case-finder/` folder into your Claude skills directory:

```bash
git clone https://github.com/afninh/use-case-finder-skill.git
cp -r use-case-finder-skill/use-case-finder ~/.claude/skills/
```

(Or drop it wherever your Claude setup loads skills from.)

## Use

Just ask, e.g.:

> "What should I build with Claude?" · "Help me find a use case." · "I don't know what to automate."

The skill will offer to look at your work and walk you through the menu.

## Portable by design

The skill carries **no user-specific data** and finds connector tools by their **name suffix** at runtime (e.g. `…__search_threads`), so it works on anyone's machine that has the same connectors enabled — no edits needed. It also degrades gracefully: if you have only some connectors (or none), it uses what's there and leans on what you tell it.

## Privacy

It reads only recent items (~30 days), samples for patterns rather than ingesting everything, asks for your go-ahead before reading anything, and writes only to your local workspace.

---

Based on the "Use-Case Framework" (Find the sting · Map the work · Pick the build).
