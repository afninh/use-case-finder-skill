# Connectors — gathering general context

Connectors are **general context**, not stage-specific inputs. Their only job here is to help you build one well-rounded, neutral portrait of how this person actually works. The framework (Stages 1–3) then draws on that whole portrait freely. **Do not** map a connector to a particular stage or sting archetype.

## How to find a connector's tools (portability)

Connector MCP tools are namespaced with an environment-specific prefix that differs per user — usually a UUID, e.g. `mcp__<some-id>__search_threads`. **The prefix is NOT stable; the suffix is.** So never hardcode a prefix.

To use a connector: scan the tools actually available to you in this session and find the one whose name **ends with** the documented suffix below. If you find it, the connector is available. If no available tool ends with that suffix, treat that connector as not connected — skip it, don't assume it's there.

This is what makes the skill portable: any user who has the same underlying connector enabled will have the same suffix, regardless of their UUID prefix. A user may have only some of these, none of them, or connectors named differently — detect what's present and use what you find.

## Scoping (keep it cheap and respectful)

- Default to the **last ~30 days** unless the user asks otherwise.
- **Sample, don't exhaust.** Pull enough to see the patterns (recurring senders, recurring meeting titles, recurring doc types) — not every item. A dozen well-chosen reads per connector usually beats a hundred.
- You are looking for **patterns and recurrence**, not contents. "She edits a doc titled 'Weekly Tracker' most Mondays" is the signal; you don't need to read the whole tracker.
- **Avoid responses that blow the token limit.** Broad "list everything" calls can return tens of thousands of tokens and fail. Prefer scoped, snippet-free queries — small `pageSize`, and flags like Drive's `excludeContentSnippets: true`. Never pull unbounded lists.
- Get the user's go-ahead before reading anything (Phase 0 in SKILL.md). Reading someone's email/Slack/files is sensitive.

## Per-connector pull recipes

For each, the suffixes to match and what general context to extract. Use read/search/list tools only — never write.

### Gmail
**Suffixes:** `search_threads`, `get_thread`, `list_drafts`, `list_labels`
**Extract (general context):**
- Who they correspond with most (recurring senders/recipients, internal vs external)
- Recurring subjects or thread patterns ("weekly update", "invoice", "[Status]")
- What's currently in flight / unanswered (a sense of the pile)
- Labels they maintain (hints at how they already try to organize)
**Cheap approach:** a few broad `search_threads` queries (e.g. `newer_than:30d`), skim subjects and senders; open a `get_thread` only when a pattern needs confirming.

### Google Calendar
**Suffixes:** `list_events`, `get_event`, `list_calendars`
**Extract:**
- Recurring meetings (title, cadence, attendees) — the rhythm of their week
- Meeting load / how much time is in meetings vs free
- Who they meet with repeatedly
**Cheap approach:** `list_events` over the last/next ~30 days; cluster by recurring title.

### Slack
**Suffixes:** `slack_search_public_and_private`, `slack_read_channel`, `slack_read_thread`, `slack_search_channels`
**Extract:**
- Channels they're active in (topics they're close to)
- Recurring asks or questions routed to them (a sense of the bottleneck)
- What kinds of messages they send repeatedly
**Cheap approach:** `slack_search_channels` to see their channels, then a couple of targeted `slack_search_public_and_private` queries for their own activity; read a channel only to confirm a pattern.

### Granola (meeting notes)
**Suffixes:** `query_granola_meetings`, `list_meetings`, `get_meetings`, `get_meeting_transcript`
**Extract:**
- Recurring meeting types and their themes
- Action items and follow-ups that recur (or that tend to vanish)
- What they consistently take notes about
**Cheap approach:** `query_granola_meetings` with a natural-language query about recent recurring topics, or `list_meetings` over ~30 days; pull `get_meetings` detail only for the recurring ones. Avoid full transcripts unless confirming something specific.

### Google Drive
**Suffixes:** `search_files`, `list_recent_files`, `read_file_content`, `get_file_metadata`
**Extract:**
- Recurring doc types they create/edit (reports, trackers, decks, proposals)
- The work products they actually produce
- What they touch most often / most recently
**Cheap approach:** prefer a scoped `search_files` (e.g. `owner = 'me' and modifiedTime > '<~30d ago>'`, exclude folders) with `excludeContentSnippets: true` and a small `pageSize` — this avoids the huge payloads `list_recent_files` can return. Use `read_file_content` only on one representative example of a recurring type to understand its shape.

## Turning pulls into the profile

Synthesize everything into one neutral portrait (`context-profile.md` in the output workspace), with a "generated on" date. Organize by what's true about their work — role/focus, recurring tasks and work products, frequent collaborators, recurring meetings, what piles up — **not** by sting archetype or build type. Every claim should cite a real signal you actually saw (e.g. "4 'weekly update' threads in 30 days"). If you didn't see evidence for something, leave it out — don't infer or fabricate.

If a connector is connected but returns little or nothing, say so plainly in the profile rather than inventing context.
