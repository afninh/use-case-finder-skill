# Gotchas — seed

These are the starting lessons that ship with the skill. They are **generic** (no user data). On first run, if the user's workspace has no `gotchas.md` yet, copy this file's body into `~/claude-use-cases/gotchas.md` and add the user's own gotchas there over time — never write user-specific gotchas back into this seed.

Read the user's `gotchas.md` (which starts as a copy of this) at the beginning of every run and let the relevant ones steer you. Append a new dated entry whenever something goes wrong or surprises you, in the format: **situation → lesson → how to avoid.**

---

## Connectors

- **Connector tool names are prefixed with an environment-specific ID (often a UUID).** → The prefix differs per user; only the suffix is stable. → Match connectors by tool-name *suffix* (e.g. `…__search_threads`), never by a hardcoded prefix. See `references/connectors.md`.

- **A connector can be "listed" but return little or nothing.** → Empty results don't mean "no patterns"; they may mean the wrong query, a permissions gap, or a quiet 30 days. → Say plainly that you found little, rather than inventing context to fill the profile.

- **It's easy to over-read and burn time/tokens.** → Reading everything doesn't make the portrait better. → Scope to ~30 days and sample for patterns; open a full thread/file/transcript only to confirm a pattern you already suspect.

- **A large connector response can blow the token limit.** → Broad "list everything" calls (e.g. Drive `list_recent_files` with snippets) can return tens of thousands of tokens and fail. → Prefer scoped, snippet-free queries (`search_files` with `excludeContentSnippets: true`, small `pageSize`); never pull unbounded lists. (Hit live during the first preview run.)

- **Not everyone has the same connectors.** → A downloader may have only some, none, or differently-named connectors. → Detect what's actually available and degrade cleanly; never assume a specific connector is present.

## Honesty & evidence

- **Every sting and every use case must cite a real signal.** → Plausible-sounding inferences feel like insight but erode trust the moment they're wrong. → If you didn't see evidence for it, don't claim it; leave it out or ask the user.

- **Get consent before reading.** → Email, Slack, files, and meeting notes are sensitive. → Confirm which connectors to use and get a go-ahead before the first read; summarize what you looked at.

## Using the framework

- **Don't funnel — never force a build.** → Marching someone from one sting straight to one build feels efficient but robs them of choice and makes them feel locked in. → Generate a *broad list* of candidates first, let the user choose what (if anything) to explore, and treat "saved for later" as a complete outcome. Going deep on any one is opt-in.

- **Capture everything, delete nothing.** → If only the discussed ideas are saved, the user loses optionality and the ones they declined vanish. → Save every generated candidate as a file + backlog row immediately; declined ones are *parked*, not deleted; started ones flip to `building`.

- **The trap is building before you've mapped.** → People wrap a Skill around a broken process and automate the inertia. → When a user *does* go deep, never recommend a build (Stage 3) for a sting that hasn't been mapped (Stage 2). Map first; the right build usually picks itself.

- **The blank-page problem applies to this skill too.** → Asking "so what do you want to build?" reproduces the very blank page the framework exists to avoid. → Lead with concrete, evidence-backed options the user reacts to, not open-ended prompts.

- **Don't dump the whole framework at once in guided mode.** → A wall of stages and lists is a lecture, not a guide. → Reveal one stage (and sub-step) at a time; finish it before moving on; let the user steer back/skip/revise.

- **Present, then pause — don't stack a decision prompt on fresh content.** → Showing the menu and immediately asking "what do you want to do?" gives no time to read; it feels rushed and pushy. → After any big reveal, stop and invite the user to read/ask/expand; wait until they signal they're ready before asking them to decide. (Hit live during the v2 preview.)

- **Don't assume the framework jargon.** → Leading with "the rebuild" / "the pile" / "the wish" (or even calling it a "tag") loses anyone who's never seen the framework. → Show the user a **"pain point"** described in plain words ("you rebuild the same deck from scratch every time"); keep the archetype labels internal (just to ensure the menu spans a range of pains), never on screen.

- **The honest gut-check before trusting a build far:** → "Can I tell when it's wrong without redoing it myself?" → If not, recommend keeping a human in the loop (chat/Project) rather than a hands-off Skill or schedule.

## Workspace

- **The skill folder may be read-only or get overwritten on update.** → Writing generated artifacts inside the skill loses them and breaks portability. → Write all user output (profile, use cases, index, living gotchas) to the runtime workspace (`~/claude-use-cases/`), never into the skill folder.
