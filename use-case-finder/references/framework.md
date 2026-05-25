# The Use-Case Framework

> Start where it stings. Then figure out what to build.

You can't find a use case by asking "what can AI do?" — that's a blank page. You find it by pointing at the part of your work that already hurts, getting honest about how it really works, and only then deciding what to build for it. Sometimes that's a chat. Sometimes it's a tool you never thought you could make.

The arc: **1 — Find the sting → 2 — Map the work → 3 — Pick the build.**

This file is the source of truth for the framework's content. The SKILL.md orchestrates *how* to walk someone through it; this file holds *what* each stage says.

## The five kinds of pain (internal coverage tool — describe as plain "pain points")

These archetype names are **for your own use**, to make sure a generated menu covers a range of pains rather than all one flavor. **Don't show these labels to the user** — instead, describe each candidate's **pain point** in plain words (a quick "what's hard today"). The names map to plain pain points like so:

- **The rebuild** → "you redo this from scratch over and over" (the weekly report, the recap).
- **The blank page** → "you dread starting this" (the proposal, the deck, the memo).
- **The pile** → "you wade through this to find what matters" (the inbox, the transcripts).
- **The bottleneck** → "only you can do this, and everyone waits on you."
- **The wish** → "you'd do this if you had more time" (the follow-ups, the analysis you skip).

---

## Stage 1 — Find the sting

**Don't hunt for a use case. Point at the situation that already grates — that's your starting task. Then name what actually hurts about it.**

Five archetypes of "the sting." Present these as the menu; each comes with everyday examples to make it concrete.

| Archetype | The situation | Examples |
|---|---|---|
| **The rebuild** | The thing you redo from scratch every week. | the report, the recap, the tracker, the update |
| **The blank page** | The thing you stare at before you can start. | the proposal, the deck, the memo, the job post |
| **The pile** | The stack you wade through to find what matters. | the inbox, the transcripts, the contracts, the replies |
| **The bottleneck** | The thing only you know how to do. | the question everyone routes to you |
| **The wish** | What you'd do if you had more time. | the analysis you skip, the follow-ups that vanish |

**The three questions for this stage (ask one at a time):**
1. Which one stings the most right now?
2. What's the pain underneath it — the time, the dread, the errors, or that it just never gets done?
3. If this got easier, what would actually change for you?

The output of Stage 1 is 1–3 named stings the person confirms, each with the pain underneath it named.

---

## Stage 2 — Map the work

**Before handing anything over, get honest about how it really works. Most people automate the task as-is — but half of it only exists out of habit. Separate what's sacred from what's just inertia, then split the rest.**

### Step A — Today: how it actually runs

Walk the real steps, start to finish, and mark where it stalls or drains.
- What are the actual steps, from trigger to done?
- Where does it slow down, break, or get boring?
- What inputs does it need, and where do they come from?

### Step B — Keep vs Drop

Sort the parts of the work into two columns.

**Keep — must stay true** (the standards and realities the result has to honor):
- Your judgment and the final call
- The voice, tone, or relationship someone expects
- Accuracy, confidentiality, the compliance lines

**Drop — doesn't need to stay true** (the bits you assume are fixed but really aren't):
- The format nobody actually reads
- Doing it manually because you always have
- Starting from a blank page every time
- You being the only one who can do it

### Step C — AI should do vs You keep

Split the remaining work.

**AI should do** (repeatable, describable, checkable):
- First drafts and rough cuts
- Sifting, sorting, summarizing the pile
- Reformatting and restructuring
- Generating options to react to

**AI shouldn't — you keep** (judgment, taste, accountability):
- The final decision and what ships
- The relationships and the read of the room
- Knowing when the output is wrong

**The two questions for this stage:**
1. What in "keep" must AI respect — and what in "drop" can it rethink entirely?
2. After the split: how much of this is AI's, and how much stays yours?

The output of Stage 2 is, per sting: the real steps, a Keep/Drop sort, and an AI-does/You-keep split.

---

## Stage 3 — Pick the build

**The shape of the work tells you what to make — and where to make it. The more of it is AI's, the more it repeats, and the more you trust it, the further down the list you go.** Then a cadence can let any build run on its own — with your connectors switched on underneath so it can reach your real work.

The four build types, in order:

| When | Build | What it is | Where |
|---|---|---|---|
| Stay close · one-off | **A chat** | You're still figuring it out, or it's a one-time thing. Think together, turn by turn. Zero setup. | Claude Chat |
| Recurring · your context | **A Project** | It keeps coming back and leans on your docs, voice, and rules. Load them once; it drafts, you spot-check. | Claude Chat — or Cowork when it touches your files & apps |
| Same job · every time | **A Skill** | It's the same task on repeat and you want it done consistently. Package it once so it runs the same way every time. | Cowork or Claude Code |
| Didn't exist before | **An app or tool** | What you actually need isn't a document — it's a small tool built for exactly your problem. The thing you never thought you could make. | An Artifact in chat — or Claude Code / API for the real build |

**The decision logic:** more of the work owned by AI + more repetition + more trust ⇒ further down the list (toward Skill / app). Less of that ⇒ stay near the top (chat / Project).

### To make any build reach further

- **A scheduled automation** — *let it run on its own.* Wrap a Project or Skill in a cadence and it runs without you — the Friday report, the morning inbox scan, the weekly digest. Set it once; come back to the result. *Where: Cowork scheduled tasks — or Claude Code / API for fully hands-off.*
- **Turn on your connectors** — *setup, not a build.* Connectors aren't something you build — they're the plumbing. Switch on email, files, Slack, and your systems once, and every build above can act on your real work instead of just advising on it.

The output of Stage 3 is, per sting: a recommended build type (and where to make it), whether to wrap it in a schedule, and which connectors it needs switched on.

---

## The closing insight (carry this throughout)

> The trap is building before you've mapped. People wrap a Skill around a broken process and **automate the inertia**. Map first — decide what must stay true and what was only ever habit — and the right build usually picks itself. And the honest gut-check before you trust it far: **can I tell when it's wrong without redoing it myself?** If not, keep your hands on it.

This is why the framework refuses to jump straight to Stage 3. Never recommend a build for a sting that hasn't been mapped.
