---
name: ambitious-prompt
description: Rewrite an ordinary task prompt into more ambitious, runnable versions along three axes — Altitude (aim at the outcome beyond the task), Depth (expert-grade methods, raw data, outside validation), and Range (borrow methods from other fields). Use when the user asks to make a prompt more ambitious, deeper, higher-level, or "less basic"; asks what Claude could do beyond the literal task; or says "프롬프트 업그레이드", "더 야심차게", "프롬프트 더 깊게", "make this prompt more ambitious", "deeper version of this task". Skip for trivial one-step tasks (typo fixes, quick lookups).
allowed-tools: Read
---

# Ambitious Prompt

Turn a plain request into a ladder of more ambitious prompts the user can paste and run.
The point is not a longer prompt. The point is a prompt that aims at a bigger outcome,
uses the methods a field-leading expert would use, and is judged by something other than the model itself.

Reply in the user's language. Keep generated prompts in the language the user will run them in
(default: the user's language; keep tool names, code, and identifiers in English).

## Axes

| Axis | What it changes | Reference |
|---|---|---|
| Altitude | Task → outcome. "What should happen after this is done? What is the goal beyond the goal?" | [references/altitude.md](references/altitude.md) |
| Depth | Same task, done the way the best professional would: rawer inputs, real instruments, hard targets, outside judge. | [references/depth.md](references/depth.md) |
| Range | Same goal, attacked with methods from other fields (verbs, not roles). | [references/range.md](references/range.md) |

Speed (same work, faster) is out of scope — it needs no prompt rewriting.

## Workflow

### 1. Intake

Extract from the conversation (ask at most 2 short questions, only if the answer changes the output):

- **Original prompt** — the literal request.
- **Purpose** — who consumes the result and what they decide or do with it.
- **Materials** — data, files, repos, MCP connectors, logs, accounts the model can actually reach.
- **Environment** — can the runner install software, execute code, run subagents, access the web?

If the task is trivial (one step, no downstream decision, no data), say so in one line,
give at most a single tightened prompt, and stop. Do not inflate small tasks.

### 2. Diagnose

Score each axis High / Medium / Low with a one-line reason. Use these signals:

- **Altitude High** when: a meeting, review, or decision follows the work; the task recurs; there is an
  obvious "next thing" the user wants to happen. **Low** for creative work valued for its own sake.
- **Depth High** when: raw data or primary sources exist; correctness can be checked by a tool, test,
  holdout set, or real-world measurement; the user cares about quality more than volume.
- **Range High** when: the output must persuade, teach, or change human behavior; rewriting the noun as
  verbs reveals several distinct skills. **Low** for narrow technical fixes.

Pick the 1–2 strongest axes. Combine them; do not force all three.

### 3. Build the ladder

Read the reference file for each chosen axis, then write three levels:

- **Lv1 — Better task.** Same scope, but with full context, raw inputs, and an outside check.
- **Lv2 — Outcome.** Aim at the decision or result the task serves.
- **Lv3 — System.** Replace or redesign the recurring process so the human leaves the loop,
  with proof from the user's own history that it would have worked.

Each level must be runnable as written. Put unknowns in `<angle-bracket placeholders>`.

### 4. Check every prompt against the rubric

Fix any prompt that fails before showing it.

- [ ] **Hard, specific target** — a number, threshold, or deadline. Never "do your best" or "improve".
      Push the target past comfortable (10s → 200ms, not 10s → 5s) and state plainly that it is solvable.
- [ ] **Raw material named** — the primary source (logs, DB tables, transcripts, crash dumps), not a digest.
- [ ] **Instruments named** — the specific methods and tools a top professional uses (e.g. SQL + survival
      model, profiler + flame graph), not just expert vocabulary.
- [ ] **Assumption challenged** — at least one belief the user holds is tested against raw data.
- [ ] **Outside judge** — something other than the model decides if it worked: tests, holdout data,
      a benchmark, a reproduction, a real measurement. No "review your own work".
- [ ] **No role play** — no "act as X" / "write like X". Replace with "do what X does: <method>".
- [ ] **Stop condition** — when to stop, and what to keep going on if it looks impossible.
- [ ] **Prerequisites listed separately** — access the runner needs but may not have. Never hide a
      missing dependency inside the prompt.

### 5. Output

Use this format:

```
## 진단 / Diagnosis
| Axis | Fit | Why |
(1 row per axis, one line each)

## Lv1 — <short name>
<prompt in a fenced block, ready to paste>
- Prerequisites: <data/tools/access needed>
- Outside judge: <what decides it worked>
- Cost: <rough size: minutes / hours / multi-session; subagents yes/no>

## Lv2 — <short name>
(same structure)

## Lv3 — <short name>
(same structure; also list the plumbing to build first so the human can leave the loop)

## Recommendation
<which level to start with and why, in 1–2 sentences>
```

When Range is chosen and the runner supports subagents, write the Range part of the prompt as
orchestration: one worker per field doing that field's method, one red-team worker, then a merge step.

## Deepen-only shortcut

If the user just wants "a deeper version" of one prompt with no ladder, run the four-question pass in
[references/depth.md](references/depth.md#four-question-pass) and return one rewritten prompt plus its
prerequisites and outside judge.

## Example

See [references/examples.md](references/examples.md) for a full before/after (quarterly business review)
and short examples for engineering and content tasks.
