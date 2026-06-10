# Retro Formats Reference

This file describes alternative retrospective formats you can use to vary the rhythm
of retros across sessions. The default format in SKILL.md (Worked Well / Didn't Work
Well / Change Ideas) is fast and practical for most sessions. These alternatives are
useful when a session was particularly complex, when the default format feels stale,
or when the user wants a different lens.

---

## Default Format: WWW (What Worked / What Didn't / What to Change)

**Best for:** Most sessions. Fast, practical, action-oriented.

```
✅ What Worked Well
❌ What Didn't Work Well
🔧 What to Change
```

This is the retro-bot default. The three columns map naturally to keep/stop/start
thinking and produce clear action items. Use this unless the user or context suggests
a different format.

---

## Format 2: Start / Stop / Continue

**Best for:** Sessions with a lot of process-level feedback, or when you want to be
explicit about new behaviors to introduce (not just fix old ones).

```
🚀 Start (things we should begin doing)
🛑 Stop (things that are wasting time or causing problems)
🔁 Continue (things that are working and shouldn't change)
```

The key difference from the default: "Start" actively invites new ideas, not just
fixes to existing problems. Good for sessions where a capability gap was the main
issue rather than an execution problem.

---

## Format 3: 4Ls — Liked, Learned, Lacked, Longed For

**Best for:** Sessions with a significant learning component, or early-stage work
where you're still figuring out the right approach together.

```
👍 Liked (what felt good and valuable)
📚 Learned (new knowledge or insights from this session)
😕 Lacked (what was missing that would have helped)
💭 Longed For (what you wish had existed or been possible)
```

"Longed For" is particularly useful for identifying new skills to build or
integrations to set up. It captures aspirational gaps, not just current failures.

---

## Format 4: Mad / Sad / Glad

**Best for:** Sessions with significant friction or frustration — when you want
to acknowledge the emotional texture of the work, not just the mechanics.

```
😤 Mad (things that were frustrating, inefficient, or wrong)
😔 Sad (things that didn't go as hoped, missed opportunities)
😊 Glad (things that made you feel good about the session)
```

This format is less common for Claude sessions but valuable when a piece of work
was genuinely difficult and the user needs to vent before problem-solving.

---

## Format 5: Sailboat / Speed Boat

**Best for:** Project-level retros covering multiple sessions, or when you want
a strategic rather than tactical lens.

```
⛵ Wind (what's pushing us forward — strengths and momentum)
⚓ Anchor (what's holding us back — recurring obstacles)
🪨 Rocks (risks ahead — things to watch out for)
🏝️ Island (the destination — what we're working toward)
```

This works well for a "quarterly retro" across a client engagement or a long-running
project, rather than a single-session retro.

---

## Choosing a Format

When the user invokes retro-bot, suggest the default format unless:
- They explicitly request a different one
- The session had a big learning component → suggest 4Ls
- There was significant frustration → suggest Mad/Sad/Glad
- You're reviewing multiple sessions at once → suggest Sailboat

You can also mix: run the default format for the tactical items, then add a "Longed
For" section at the end to capture bigger aspirational gaps.

---

## Timebox Guidance

| Format | Suggested time |
|---|---|
| WWW (default) | 10–15 min |
| Start/Stop/Continue | 10–15 min |
| 4Ls | 15–20 min |
| Mad/Sad/Glad | 15–20 min |
| Sailboat | 20–30 min |

The retro itself should be fast and focused. If you're spending more than 20 minutes
on a single-session retro, you're likely trying to solve problems in the retro rather
than simply identifying and logging them. Keep the problem-solving for the action item
application phase.
