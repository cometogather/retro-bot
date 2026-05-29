---
name: retro-bot
description: >
  Run an agile-style sprint retrospective on a completed Claude collaboration session.
  Use this skill after finishing a piece of work with Claude — a scope of work, a data
  analysis, a content build, a code session, a Cowork task — to reflect together on what
  worked, what didn't, and what to change. Triggers on: "let's do a retro", "run a retro",
  "retrospective", "retro-bot", "what worked well", "what could we improve", "session
  review", "what should we do differently", "let's debrief", or any request to reflect on
  a completed Claude session and extract improvements. The skill produces a collaborative
  retro board, maps issues to actionable file changes (skill updates, Claude.md edits,
  process changes), applies those changes using proper versioning, and saves a dated
  snapshot to a user-configured archive directory — building a permanent audit trail of
  every retro run and its outcomes. Always use this skill rather than improvising a retro.
---

# Retro-Bot

A skill for running lightweight agile retrospectives on Claude collaboration sessions —
making the process of working with Claude incrementally better over time.

The core loop: after you and Claude finish a piece of work, you take a few minutes to
ask three questions together:
- **What worked well?** (keep doing this)
- **What didn't work well?** (friction, rework, confusion, wasted tokens)
- **What should we change?** (concrete improvements to skills, prompts, or process)

Changes are applied immediately and every retro is saved as a snapshot to a persistent
archive. Over time, this builds a running audit trail of how your Claude workflow has
evolved — and compounds into a setup that gets meaningfully faster with each session.

---

## Phase 0 — Archive Directory Setup (first run only)

Before the retro begins, check whether a retro archive directory has been configured.
Look in Claude.md for a block like this:

```
## Retro-Bot
archive_dir: [path]
```

**If it's already set:** proceed directly to Phase 1. No need to ask again.

**If it's not set:** ask the user once, clearly:

> "Before we start — where do you want to save retro snapshots? This is a one-time
> setup. Give me a folder path (e.g. `H:\My Drive\Retros` or `~/Documents/retros`)
> and I'll save every retro there automatically going forward."

Once the user provides a path:
1. Add the following block to Claude.md (create the file if it doesn't exist):
   ```
   ## Retro-Bot
   archive_dir: [the path they gave you]
   ```
2. Create the directory if it doesn't exist
3. Create an empty `retro-log.md` in that directory (see Phase 6 for its format)
4. Confirm: "Got it — retro archive set to `[path]`. All future retros will save there."

Then continue to Phase 1.

---

## Phase 1 — Read the Session Context

Read the session transcript to understand what actually happened. If your environment
provides a session history or transcript tool, use it now to pull the full record of
what occurred. (In Cowork, this is available automatically; in Claude Code, use
`/transcript` or equivalent if available.) Even without the full transcript, pull from
what you know: which skills were used, what files were created, what feedback the user
gave mid-session, where things had to be redone.

If the user invokes this skill immediately after a session, you already have the context.
If they invoke it later with a description, work from that.

Ask the user to confirm what session/work they want to retro on if it isn't clear.

---

## Phase 2 — Claude Opens with Observations

Go first. Don't wait for the user to list complaints — share what *you* noticed. This
models good retrospective behavior, shows you were paying attention, and often surfaces
things the user didn't consciously register but will recognize immediately.

Frame observations honestly and specifically:

- "I noticed I had to re-render the SOW twice because the first table format didn't open
  cleanly in Word — that's a skill configuration issue I can fix."
- "You gave me the client brief in three separate messages rather than one block —
  that's worth noting as a workflow pattern that slows things down."
- "The scope builder and SOW builder skills produced consistent numbers — that felt smooth."
- "I wasn't sure which export format you needed until you told me midway through — a
  quick upfront question would have saved a round trip."

Keep it to 3–5 observations. Be direct, not defensive. You're a participant, not a witness.

---

## Phase 3 — Invite the User's Input

After your opening, invite the user to add, amend, or push back:

> "Those are my observations. What's on your list — anything I missed, anything you'd
> frame differently, or things you want to make sure we capture?"

The user's friction points are often different from yours. They may flag things that
were confusing, output quality issues they didn't mention in the moment, process
annoyances, or things that felt great and should be preserved. Capture everything.

---

## Phase 4 — Build the Retro Board

Once you've both contributed, present the full board. Be specific — vague items don't
produce useful action items.

```
## ✅ Worked Well
- [specific thing that went smoothly]
- ...

## ❌ Didn't Work Well
- [specific friction point, root cause if known]
- ...

## 🔧 Change Ideas
- [concrete suggestion tied to a "didn't work well" item]
- ...
```

Ask the user to confirm before moving on:
> "Does this capture it? Anything to add or adjust before we figure out what to act on?"

---

## Phase 5 — Map to Action Items

For each Change Idea, determine the type and priority:

| Type | When to use |
|---|---|
| 🔧 **Skill update** | Issue came from a skill's instructions, output format, or default behavior |
| 📋 **Project/session update** | Context or instruction scoped to a specific project, client, or session type — not global |
| 📝 **Claude.md update** | Missing context that applies everywhere, across all projects and sessions |
| 💡 **Process note** | Behavioral change — no file edit needed, just a different way of working |
| 🆕 **New skill** | Gap is recurring and large enough to warrant its own skill |

The key distinction between a project/session update and a Claude.md update is **scope**.
If the context should apply *only when working on a specific project, client, or in a
specific session type*, it belongs at the project/session layer. If it should apply
always, everywhere, for the user across every piece of work, it belongs in Claude.md.
Getting this wrong is costly either direction: too much in Claude.md creates noise and
context bleed between clients; too much in project files means you have to re-set context
every time you switch projects.

For each action item, state what changes, where, why it matters, and whether to act now
or note for later. Confirm before applying anything:

> "Here's what I'm proposing to change. Want me to go ahead?"

See `references/action-item-types.md` for detailed guidance on each type.

---

## Phase 6 — Apply Changes with Versioning

Apply each confirmed action item using a copy-first versioning pattern — never
overwrite the source file directly. The rule: read current → apply edits in memory →
write to a new version filename (e.g., `SKILL-v1.1.md`) → keep the old file in
`archive/`. This creates a recoverable history without a separate versioning tool.

**Skill updates:** Read current → apply in memory → write to new version filename →
archive old → add change log entry. Bump patch for small fixes, minor for meaningful
additions, major for architecture changes.

**Project/session updates:** Identify the right instruction file for the scope of the
change — this could be a project-level `CLAUDE.md` at a repo or folder root (Claude Code),
a Cowork session configuration, a standing brief file for a recurring client engagement,
or custom instructions scoped to a session type. If the file doesn't exist, create it.
Apply the same copy-first pattern as any other file change.

Common targets:
- `[project-folder]/CLAUDE.md` — loaded automatically in every Claude Code session for that project
- A `[client-name]-brief.md` or `[project-name]-context.md` standing reference file
- Cowork session-level configuration or system prompt
- Claude.ai Custom Instructions (account settings → "What would you like Claude to know")

**Claude.md updates:** Read current → add new context in the right section → write
new version → archive old. If no Claude.md exists, create one.

**Process notes:** Document in the retro snapshot (no separate file needed).

After applying, confirm what changed:
> "Done — updated [skill name] to v1.1 and added a note to Claude.md about [topic]."

---

## Phase 7 — Save the Retro Snapshot and Update the Audit Log

This phase is mandatory — every retro run must produce a saved snapshot, regardless
of how many action items were applied. The snapshot is the record; the audit log is
the feed.

### Step 1: Save the Retro Snapshot

Save a full retro snapshot to the configured `archive_dir`. Filename format:

```
[archive_dir]/YYYY-MM-DD-[short-descriptor]-retro.md
```

Example: `H:\My Drive\Retros\2026-05-15-doc-build-retro.md`

Keep descriptors short (3–5 words, hyphenated): `dashboard-build`, `content-draft`,
`data-analysis-q2`.

### Snapshot Template

```markdown
# Retro Snapshot: [Session Descriptor]
**Date:** YYYY-MM-DD
**Session type:** [SOW build / data analysis / content / code / other]
**Skills used:** [comma-separated list]
**Retro format:** [WWW / Start-Stop-Continue / 4Ls / etc.]

---

## ✅ Worked Well
- [item]

## ❌ Didn't Work Well
- [item]

## 🔧 Change Ideas Discussed
- [item]

---

## Action Items & Outcomes

| # | Change | Type | Target | Status |
|---|---|---|---|---|
| 1 | [description] | Skill update | [skill] v1.0 → v1.1 | ✅ Applied |
| 2 | [description] | Project/session update | [project CLAUDE.md / client brief / session config] | ✅ Applied |
| 3 | [description] | Claude.md update | Claude.md | ✅ Applied |
| 4 | [description] | Process note | — | 📝 Noted |
| 5 | [description] | New skill | [name] | 🔜 Backlogged |

---

## Process Agreements
[Any behavioral agreements made during this retro — things both parties agreed to do
differently next time, that don't map to a file change]

## Open Questions / Backlog
[Items noted for later, things to revisit, or follow-ups from this retro]

## Notes
[Any additional context worth preserving]
```

### Step 2: Update the Audit Log

After saving the snapshot, append one line to `retro-log.md` in the archive directory.
This file is the running feed — a single glanceable record of every retro ever run.

**retro-log.md format** (create with this header on first run):

```markdown
# Retro Log

Running record of all retro-bot sessions.

| Date | Session | Applied | Noted | Backlogged | Snapshot |
|---|---|---|---|---|---|
```

Append each new retro as one row:

```markdown
| 2026-05-15 | Doc build – long-form proposal | 2 | 1 | 0 | [link](2026-05-15-proposal-doc-retro.md) |
```

- **Applied**: number of action items with status ✅ Applied
- **Noted**: number of process notes (📝 Noted)
- **Backlogged**: number of items marked 🔜 Backlogged

After saving both files, confirm:
> "Retro snapshot saved to `[archive_dir]/[filename]` and the audit log updated.
> You now have [N] retros on record."

---

## Tone and Spirit

- **Claude goes first** — share your observations before asking for the user's.
- **Be specific** — "the `.docx` table didn't render because column widths were hardcoded"
  is more useful than "the file format was wrong."
- **Small changes compound** — a 3-line fix that saves 10 minutes per session adds up fast.
- **Not everything needs fixing** — two well-chosen changes beat eight half-hearted ones.
- **Keep it fast** — aim for 10–15 minutes. If it's running long, you're solving problems
  in the retro rather than identifying them. Save the solving for Phase 6.

---

## Reference Files

- `references/retro-formats.md` — Alternative formats: 4Ls, Start/Stop/Continue,
  Mad/Sad/Glad, Sailboat. Read when the user requests a different format or when variety
  would serve the session better than the default WWW.
- `references/action-item-types.md` — Detailed guidance on skill update vs. Claude.md
  vs. process note vs. new skill. Read when an action item's type is ambiguous.

---

## Change Log

| Version | Date | Change |
|---|---|---|
| v1.0 | 2026-05-26 | Initial version — full retro workflow, 6-phase structure, copy-first versioning, retro report template |
| v1.1 | 2026-05-26 | Added Phase 0 archive directory setup (one-time config saved to Claude.md), mandatory retro snapshot saving, running audit log (retro-log.md) with per-retro outcomes tracking |
| v1.2 | 2026-05-26 | Added project/session update as a distinct action item type — covers project CLAUDE.md, Cowork session config, client brief files, and Claude.ai Custom Instructions; clarified scope distinction from user-level Claude.md |
| v1.3 | 2026-05-29 | Migrated to plugin structure (skills/retro-bot/SKILL.md), added .claude-plugin/plugin.json for Claude Code compatibility |
