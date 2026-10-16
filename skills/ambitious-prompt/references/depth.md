# Depth — do it the way the best in the field would

Depth keeps the task the same size but raises the craft until even field experts might learn something.
Models asked to "act like a professional" tend to switch vocabulary without switching methods. Depth
prompts name the methods.

## Five techniques

1. **Use the instruments of the best.** Name the actual tools: a database and SQL instead of markdown
   tables, a statistical model instead of eyeballing, a profiler instead of guesses, a real renderer
   instead of a description. The user does not need to know them — ask the model to pick and name them.
2. **Set an unreasonable target and call it reasonable.** Multiply the ambition (5s load → 200ms, 10%
   lift → 2×). If the model says it is impossible, the prompt already says: it is solvable, keep going,
   and report what was tried.
3. **Challenge what we "know".** Business beliefs are approximations. Give raw data and ask to reproduce
   the belief adversarially: "We believe churn is an onboarding problem. Try to reproduce that from the
   raw event logs; if it doesn't hold, say what does."
4. **Produce new knowledge.** Once deep in the data, ask for a blind spot and proof: "Build a simulation
   that reproduces last year from our logs, find the earliest churn signal we don't know about, and show
   it predicts on data it has not seen."
5. **Use an outside judge.** The model does not grade itself. Prefer a tool it can run for immediate
   feedback: test suite, holdout set, benchmark, reproduction script, lint/type-check, real measurement,
   a second independent model run blind.

## Raw-material ladder

Move the input one step closer to the source:

summary/report → spreadsheet export → database tables → event logs / transcripts / crash dumps → the
system that produces them (instrument it).

## Four-question pass

Use this when the user wants one deeper prompt rather than a ladder. Answer each briefly, then rewrite:

1. What would a top professional in this field do here that the user is not asking for?
2. What is the rawest material they would start from, instead of what has already been digested?
3. Which specific methods and tools would they use?
4. What, other than the model or the user, would show the result is right?

Then rewrite the user's prompt to ask for exactly that, and check it against the rubric in SKILL.md.

## Phrasing patterns

- "Load <raw source> into <DuckDB/SQLite/Postgres> and work from queries, not summaries."
- "Fit <model type> and report effect sizes with confidence intervals."
- "Target: <aggressive number>. This is achievable; if you hit a wall, list what you tried and keep going
  on the most promising path."
- "Hold out <period/segment>. Only claim a finding if it holds on the holdout."
- "Done means <tool> passes / <metric> reaches <value> on <independent check>."
