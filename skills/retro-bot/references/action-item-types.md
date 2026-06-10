# Action Item Types — When and How to Apply Each

When a retro surfaces something worth changing, map it to the right type of change
before acting. The wrong vehicle produces the right intent but no lasting effect.

---

## 🔧 Skill Update

**Use when:** The issue traces back to a skill's instructions, output format, default
behavior, assumptions, or missing edge-case handling.

**Signs it's a skill issue:**
- "The file came out in the wrong format" → skill needs a different export step
- "Claude asked too many clarifying questions" → skill is over-prompting
- "The output was too long / too short" → skill needs output length guidance
- "It re-did a step I'd already done" → skill lacks a check for existing work
- "The table headers were wrong" → skill has hardcoded assumptions

**How to apply:**
1. Identify the specific skill
2. Identify the specific section or instruction to change
3. Apply copy-first versioning:
   - Read current version → apply edits in memory → write to new version filename
   - Bump version (patch for small fixes, minor for meaningful additions)
   - Add change log entry
   - Move the old version to `archive/` — never overwrite the source directly
4. Confirm to the user what changed and why

**Version bump guide:**
| Change size | Bump |
|---|---|
| Typo fix, minor wording | patch: v1.0 → v1.0.1 (or just v1.1 if using 2-part versioning) |
| New instruction, edge case handling | minor: v1.0 → v1.1 |
| Restructured workflow, new phase | major: v1.0 → v2.0 |

---

## 📋 Project/Session Update

**Use when:** The issue reflects missing or incorrect context that's scoped to a specific
project, client engagement, or session type — not something that should apply globally
across all work.

**The core question:** "Would I want this instruction active when working on a completely
different project or for a different client?" If yes → Claude.md. If no → project/session layer.

**Signs it's a project/session issue:**
- "Claude didn't know this client's preferences or constraints" → add to a client brief file
- "I had to re-explain the project's tech stack or folder structure every session" → project CLAUDE.md
- "The Cowork session kept defaulting to behaviors that don't fit this engagement" → session config
- "Context from Project A bled into Project B" → the context is in the wrong layer (too global)
- "I always want X when working in this repo, but not in other repos" → project CLAUDE.md at repo root

**The instruction layers available:**

| Layer | Lives in | Loaded when |
|---|---|---|
| Claude Code project | `CLAUDE.md` at repo/folder root | Every Claude Code session in that directory |
| Client/engagement brief | `[client]-brief.md` or `[project]-context.md` | Referenced explicitly, or auto-loaded via Claude.md |
| Cowork session config | Cowork system prompt or session instructions | Every Cowork session of that type |
| Claude.ai Custom Instructions | Account settings → "What would you like Claude to know" | Every claude.ai chat session |

**How to apply:**
1. Identify which layer is right for the scope of the change
2. Find or create the file (project CLAUDE.md, client brief, etc.)
3. Add the specific, actionable instruction — same writing standard as Claude.md (facts, not wishes)
4. Apply copy-first versioning: read current → edit in memory → write to new version filename → move old to `archive/`
5. Confirm to the user what was added and where

**The scope hygiene principle:** Resist putting client-specific context into the global
Claude.md. When you work with 5+ clients, a bloated Claude.md full of per-client details
creates noise and potential confusion. Each client deserves their own clean context file.

---

## 📝 Claude.md Update

**Use when:** The issue reflects missing or incorrect context that Claude needed
about the user, project, preferences, or working environment — context that applies
*across* sessions, not just to one skill.

**Signs it's a Claude.md issue:**
- "Claude didn't know I always want files in H:/..." → add persistent path preference
- "I had to re-explain the client context twice" → add client/project context block
- "Claude didn't know my role or company" → add user/company context
- "Claude kept using formal language when I prefer casual" → add tone preference
- "I always need output in .docx, not .pdf" → add format preference

**How to apply:**
1. Identify what context is missing
2. Determine the right section of Claude.md (or create one)
3. Write a clear, specific addition — not vague preferences but actionable facts
4. Version the Claude.md file

**Good Claude.md additions look like:**
```
## File Output Preferences
- Always save final deliverables to H:/My Drive/[path] unless instructed otherwise
- Default document format: .docx unless user specifies PDF
```

**Poor Claude.md additions:**
```
- Be more careful next time
- Try to do better
```

---

## 💡 Process Note

**Use when:** The fix is behavioral — a change to how you and the user approach a
type of work — not a change to a file. Process notes don't require editing anything;
they're reminders and agreements.

**Signs it's a process issue:**
- "I should have given Claude all the brief context in one message, not three"
- "We should agree on the output format before Claude starts building"
- "I should run the retro immediately after delivery, not a week later"
- "Claude should always ask which client folder to save to before creating files"

**How to apply:**
Document process notes in the retro report under a "Process Agreements" section.
You can also add persistent process notes to Claude.md if they're important enough
to enforce across all sessions.

**Example retro report section:**
```markdown
## Process Agreements
- Provide full brief in a single message block before starting builds
- Claude will confirm output path before creating any deliverable file
- Retros should be run within 24 hours of session completion
```

---

## 🆕 New Skill Needed

**Use when:** A recurring gap is large enough and specific enough to warrant its own
skill — not a patch to an existing one.

**Signs a new skill is warranted:**
- The same type of work comes up repeatedly and always has the same friction
- The current approach is a workaround cobbled together from multiple skills
- There's a coherent, bounded workflow that doesn't fit any existing skill
- The user says "I wish there was a skill for X"

**How to apply:**
1. Note it as a "🆕 New skill: [name]" action item in the retro report
2. Describe in 2–3 sentences: what it would do, when it would trigger, what problem it solves
3. If deferring, the retro report acts as the backlog item

**Threshold:** Don't create a new skill for something that happens once or is
addressable with a small SKILL.md edit. New skills are overhead. The bar should
be: "we'll do this type of work at least 5–10 more times and it always has this gap."

---

## Priority Triage

Not every action item should be acted on immediately. Use this quick triage:

| Priority | Criteria | Action |
|---|---|---|
| **Act now** | Recurring issue, easy fix, high token/time cost | Apply in this session |
| **Note for later** | Valid issue, complex fix, low frequency | Log in retro report |
| **Won't fix** | Edge case, one-time issue, acceptable tradeoff | Note why, close it |

Aim for 1–3 "Act now" items per retro. More than that and you're overloading a single
session. The retro report is your backlog — items don't disappear, they wait.
