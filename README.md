```
   .------------------------------------------------.
   | retro-bot says: "Always leave things better    |
   | than you found them!"                          |
   '------------------------------------------------'
        \
         |
        [■]
    .----------.
    |[══]  [══]|
    |          |
    | .------. |
    | |======| |
    '----------'
  .-------------.
  |             |
  | ✓  | ✗ | ↻ |
  |   retro-bot |
  '-------------'
      ||   ||
     _||   ||_
    [__]   [__]
```

# retro-bot

> *"Always leave things better than you found them."*

**An open-source agile retrospective skill for Claude.**
Make your AI sessions compound.

[![Install skill](https://img.shields.io/badge/Install%20skill-retro--bot%20v1.2-blue)](./retro-bot.skill)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)
[![Built with Claude](https://img.shields.io/badge/Built%20with-Claude-orange)](https://claude.ai)

---

## The problem

If you've worked in Agile, working with Claude should feel familiar. Especially as a
product owner, your core skill is articulating what you want built, and that maps
directly to getting great outputs from Claude. The clearer the brief, the better the
output. Same principle, different medium.

I've found one valuable element from Agile that was missing for me: the retrospective.

Retrospectives are the point of origination for iteration. It's where you clear the air,
get on the same page, align on what worked and what didn't, and commit to the specific
changes that carry those lessons forward. It invites self-reflection and a collective
approach to improvement. In a Claude workflow, its value can compound due to the more
rapid cycles of creation and iteration.

Without a deliberate improvement loop, every session carries the same overhead. You
re-establish context that should already be there. You hit the same friction you hit
last week. Learnings either evaporate or get dumped into one bloated file that creates
its own problems. Token budgets inflate. Output quality plateaus, and you end up with
an inflated, unwieldy prompt instead of a systemic approach to incremental improvement
in the right places.

Most people optimize the prompt. The best teams optimize the process.

retro-bot brings the retrospective loop to Claude.

---

## What it does

After any Claude session, retro-bot runs a structured retrospective with you, and
then does something most people haven't thought about: it routes each improvement to
exactly the right layer of your Claude setup.

There are four places where context and instructions live in a Claude workflow:

| Layer | What lives here |
|---|---|
| 🔧 Skill | How a specific capability is configured |
| 📋 Project | What Claude knows about this engagement |
| 📝 Claude.md | Persistent context that applies across all sessions |
| 💡 Process | Behavioral agreements: how you and Claude work together |

Most people know they should "update their prompts" after a session. What's less
obvious is *where* the fix belongs. Without a clear answer, everything ends up
dumped into one bloated global file. retro-bot figures out the right scope and applies
the change on the spot, versioned and recorded. That's the part most retro frameworks
skip. retro-bot doesn't.

```
✓  What worked well      →  keep doing this
✗  What didn't work      →  find the root cause
↻  What to change        →  apply it to the right layer, right now
```

Every retro saves a dated snapshot. A running audit log tracks every session, every
improvement, every outcome: a permanent record of how your Claude setup has evolved
and why.

After ten retros, you can look back and see exactly how your setup has evolved. The
prompts are tighter. The skills are smarter. The sessions are faster. That's
compounding.

---

## The audit trail

This is what your retro log looks like after a few sessions:

```markdown
# Retro Log

| Date       | Session                         | Applied | Noted | Backlogged | Snapshot |
|------------|---------------------------------|---------|-------|------------|----------|
| 2026-05-15 | SOW build – consulting client   | 2       | 1     | 0          | [→](retros/2026-05-15-consulting-sow-retro.md) |
| 2026-05-18 | Dashboard – internal ops        | 2       | 0     | 1          | [→](retros/2026-05-18-ops-dashboard-retro.md) |
| 2026-05-22 | Campaign brief – client         | 1       | 2     | 0          | [→](retros/2026-05-22-campaign-brief-retro.md) |
| 2026-05-26 | Data analysis – Q2 review       | 3       | 0     | 1          | [→](retros/2026-05-26-q2-analysis-retro.md) |
```

Each row links to a full snapshot: the retro board, every action item, what was applied,
what was deferred, and any process agreements made. It's a record of how the workflow
actually evolved: what stuck, what got reversed, what compounded. Nothing disappears.

---

## How a session looks

You finish a piece of work. You type:

> *"let's do a retro on that session"*

retro-bot goes first. Before asking for your input, it opens with blunt
self-observations about what it noticed in the session. That's intentional: it breaks
the sycophancy default, models honest self-assessment, and usually surfaces things you
noticed but didn't say out loud. Then you build the board together, map issues to
specific file changes, apply them with versioning, and save the snapshot.

A typical retro takes 10-15 minutes. The output is a versioned skill update, a Claude.md
addition, or a process note, plus the dated snapshot in your archive.

**Example exchange:**

> **Claude:** Before you weigh in: here's what I noticed. The SOW table didn't render
> cleanly in Word on the first pass; I had to rebuild it. That's a skill config issue I
> can fix. I also wasn't sure which folder to save to until you told me mid-session.
> A quick upfront question would have saved a round trip. On the positive side, the
> staffing numbers stayed consistent across the scope spreadsheet and the SOW doc.
> What's on your list?
>
> **You:** Yeah the folder thing kept happening last week too. Can we make that automatic?
>
> **Claude:** Good catch. That's a Claude.md update, not a skill update. I'll add your
> default output path so it's set for every session. Proposing two changes total: patch
> the table format in the SOW skill, and add the path preference to Claude.md. Want me
> to apply both now?

---

## Retro formats

The default is WWW (What Worked / What Didn't / What to Change). Fast and practical
for most sessions. retro-bot also supports:

- **Start / Stop / Continue**: when you want to explicitly introduce new behaviors
- **4Ls: Liked, Learned, Lacked, Longed For**: when the session had a big learning component
- **Mad / Sad / Glad**: when you need to name the frustration before solving it
- **Sailboat**: for multi-session or quarterly reviews; strategic rather than tactical

---

## Prerequisites

retro-bot is self-contained, with no dependencies on other skills or external services.

**Required:**
- **Claude Code** or **Cowork** (Claude desktop): the environments retro-bot runs in
- **File system access**: so Claude can read and write skill files, instruction files, and retro snapshots
  - *Cowork:* connect a folder via the workspace selector before running a retro
  - *Claude Code:* file access is automatic within your project directory

**Optional but recommended:**
- [**Desktop Commander**](https://desktopcommander.app/): gives Claude broader file system access across your machine, useful if your skills or retro archive live outside the connected folder

No accounts. No APIs. No additional installs.

---

## Install

### Cowork (Claude desktop)

1. Download [`retro-bot.skill`](./retro-bot.skill)
2. Open Cowork → click the **+** button → **Install skill from file**
3. Select `retro-bot.skill`
4. Done. Trigger it by saying *"let's do a retro"* after any session.

**First run:** retro-bot will ask you to set an archive directory once, a folder
where all retro snapshots will be saved automatically going forward.

### Manual install (Claude Code / advanced)

```bash
git clone https://github.com/cometogather/retro-bot.git
```

Then add the skill path to your Claude Code config. In `.claude/settings.json`:

```json
{
  "skills": ["/absolute/path/to/retro-bot"]
}
```

Or reference it from your project `CLAUDE.md`:

```markdown
## Skills
- /absolute/path/to/retro-bot
```

---

## What's inside

```
retro-bot/
├── SKILL.md                        ← the skill (7-phase retro workflow)
├── references/
│   ├── retro-formats.md            ← WWW, 4Ls, Start/Stop/Continue, etc.
│   └── action-item-types.md        ← when to use each type of change
├── retros/                         ← default archive placeholder (your snapshots
│                                      go wherever you configure in Phase 0)
├── archive/                        ← old skill versions (copy-first versioning)
├── .gitignore                      ← keeps personal retros out of your fork
├── LICENSE                         ← MIT
└── README.md                       ← you are here
```

---

## The philosophy

Shared understanding breeds collective iteration.

I built retro-bot because I noticed many components of Agile applied to how I
approached my work with Claude. I found myself missing the retrospective loop I would
run in my IRL agile teams. I needed a structured way to make things better, get rid of
repetitive corrections, and continue the feedback loop.

What wasn't obvious at first was what to do with the insights once you have them.
Claude has multiple layers where improvements can live: the skill level, the project
level, the global memory, the persistent context file. Getting the right fix to the
right layer is what makes the improvement stick. That's the part most retro frameworks
skip. retro-bot doesn't.

I work with Claude every day at [Gather](https://gather.co): scope of work builds,
briefs, data analyses, content, research. The retro loop is how I make sure each
session teaches me something that makes the next one faster, sharper, and cheaper
in tokens.

I'm sharing this publicly because if it improves your outcomes, your token efficiency,
and the quality of your outputs, we all stand to benefit. Shared understanding breeds
collective iteration. That only works if the loop is open.

This is a work in progress. Use it, fork it, improve it, run it back through itself,
and pay it forward when you can.

---

## Version history

| Version | Date | What changed |
|---------|------|--------------|
| v1.2 | 2026-05-26 | Added project/session update type (project CLAUDE.md, client briefs, session configs) |
| v1.1 | 2026-05-26 | Archive directory setup, mandatory snapshots, running audit log (retro-log.md) |
| v1.0 | 2026-05-26 | Initial release: 7-phase retro workflow, 5 formats, copy-first versioning |

---

## Contributing

Feedback is always welcome. If you use retro-bot and find something worth improving,
open a PR or an issue. Describe the friction, propose the fix. That's the whole
methodology applied to itself.

---

## Built by

**Christophe Jammet**, AI enablement and systems design  
[linkedin.com/in/cjammet](https://linkedin.com/in/cjammet) · [github.com/CR8-OS](https://github.com/CR8-OS)

Purpose built for [**Gather**](https://gather.co), a collective of independent thinkers,
creators and practitioners who move at the velocity your business demands.  
[github.com/cometogather](https://github.com/cometogather)

---

*"Bite my shiny metal audit trail."*
