# Range — borrow methods from other fields

Range attacks the same goal with knowledge, tools, and techniques from fields the task does not obviously
need. It used to be uneconomical to staff all of them; with subagents it is cheap.

## Step 1 — Replace nouns with verbs

Rewrite the deliverable as what it has to *do*. The verbs reveal which fields matter.

- "A QBR deck" → "get busy people to believe a cause-and-effect story and decide under uncertainty in
  30 minutes."
- "A landing page" → "make a stranger understand, trust, and act within 10 seconds."
- "A bug fix" → "find why a system behaves differently from what its authors believe, and prevent it
  recurring."

## Step 2 — Assemble the crew

Ask: if this had to be extraordinary (stakes: "or the aliens blow up Earth"), which specialists would you
hire? Aim for 3–6, including at least one adversary. Example for the QBR:

| Field | What they bring (a method, not a voice) |
|---|---|
| Analyst | Decompose metric changes into drivers; variance analysis |
| Journalist | Find the single lede; verify every claim against a source |
| Editor | Cut to the argument; enforce one idea per slide |
| Motion / audio designer | Pacing and emphasis if it is presented |
| Short seller (red team) | Build the bear case: what is the company hiding from itself? |
| Forensic accountant (red team) | Reconcile numbers to source; look for flattering definitions |

## Step 3 — Methods, not role play

Role play makes transcripts weirder without improving results. Convert each crew member into a task:

- ✗ "Write this like a short seller."
- ✓ "Do what a short seller does to research a position: find the three metrics management would least
  want scrutinized, trace each to raw data, and write the bear case."

## Orchestration template

When the runner supports subagents, phrase Range as:

```
Run these workstreams in parallel, each as its own subagent with access to <materials>:
1. <Field A>: <method> → deliver <artifact>
2. <Field B>: <method> → deliver <artifact>
3. Red team (<adversarial field>): <method> → deliver the strongest case against the draft
Then merge: resolve conflicts explicitly, keep only claims that survived the red team, and list what was
dropped and why.
```

## Spotting unconsidered fields

Prompt the model to suggest crafts the user has not thought of (e.g. 3D rendering for interior design,
game-engine tooling for a homepage, epidemiology methods for churn). Ask for 2–3 surprising candidates,
each with the concrete technique it would contribute.
