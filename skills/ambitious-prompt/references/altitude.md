# Altitude — aim at the outcome, not the task

A task prompt is the user's best guess at how to reach an outcome. Altitude asks the model to own the
outcome instead. Example of the shift: "fix this crash" → "keep our apps crash-free".

## Finding the goal beyond the goal

Ask, in order, and stop at the first level the materials and environment can support:

1. **What changed / what is true?** The task's literal output, but with all available context.
2. **What should be decided?** Most work feeds a decision. Find the 2–3 most urgent decisions and prepare
   options with arguments for and against each.
3. **Why does this process exist at all?** Name the underlying purpose (e.g. "leadership catches problems
   early and moves money and people"). Design a better mechanism for that purpose, prove from the user's
   own history that it would have caught things sooner, and run it alongside the current process.

Tell-tale sign that Altitude fits: there will be a meeting about this work. Weak fit: creative work valued
for its own sake.

## Phrasing patterns

- "Tell me what changed, why, and what we should do about it." (not "update the numbers")
- "Work out which <N> decisions are most urgent given everything you learned, and draft directions for
  each with for/against arguments."
- "<Process> exists so that <purpose>. Design a better way to achieve that than <current artifact>,
  backtest it on our last <period> of history to show it would have caught <X> sooner, and run it beside
  the current one for <period>."
- "Own <outcome metric>. Keep it at <target> without me assigning individual tasks."

## Taking the human out of the loop (Lv3)

A standing outcome only works if the model can see, act, and verify on its own. List the plumbing as
prerequisites, for example:

- **See**: reliable access to the signal (crash reports, metrics DB, CRM export, inbox).
- **Map**: link signals to causes (app version → git commit, campaign → revenue line).
- **Act**: permission and tooling to make the change (repo write, deploy, draft mode in a CMS).
- **Verify**: an independent way to reproduce and confirm the fix (test machines per OS, staging, holdout).
- **Report**: a cadence and channel for what was done and what needs a human.

If any of these is missing, the Lv3 prompt's first step is to build or request it.

## Limits

"Go make money" style prompts are still too open in 2026. Keep the outcome bounded by a metric, a scope,
and a time window.
