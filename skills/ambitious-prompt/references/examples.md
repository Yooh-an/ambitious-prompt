# Examples

## 1. Quarterly business review (full ladder)

**Original:** "Fill in our QBR template with this quarter's numbers."

**Diagnosis:** Altitude High (a leadership meeting and budget decisions follow). Depth High (raw
billing/usage data exists; churn claims can be backtested). Range Medium (the deck must persuade).

**Lv1 — Explain the quarter**
```
Here is everything I can get: <billing export>, <product event logs>, <CRM pipeline>, <last 4 QBR decks>.
Load the raw data into DuckDB and work from SQL, not the decks.
Tell me what changed this quarter, why, and what we should do about it. For every "why", show the query
and the effect size. We currently believe churn is an onboarding problem — try to reproduce that from the
raw logs and say plainly if it doesn't hold.
Then fill <template> with the findings.
Done = every number in the deck reconciles to a query in an appendix.
```
- Prerequisites: exports above; DuckDB installable.
- Outside judge: appendix queries re-run to the same numbers; finance spot-checks 3 figures.
- Cost: ~1–2 hours, single session.

**Lv2 — Prepare the decisions**
```
<Lv1 context>
Work out which three decisions are most urgent given everything you learned. For each: two or three
directions, for/against arguments backed by our data, and what we would need to see next quarter to know
we chose right.
Run the analysis as parallel workstreams: (1) variance analysis of revenue drivers, (2) find the single
story leadership must believe and verify each claim against source, (3) red team — research the bear case
the way a short seller would: the three metrics we'd least want scrutinized, traced to raw data.
Merge, keeping only claims that survived the red team.
```
- Prerequisites: as Lv1; subagents available.
- Outside judge: red-team findings addressed in writing; holdout check on any predictive claim.
- Cost: half a day, multi-agent.

**Lv3 — Replace the QBR**
```
The QBR exists so leadership catches problems early and moves money and people to the right places.
Design a better mechanism for that than a quarterly deck. Backtest it on our last 8 quarters of raw data
and show which problems it would have flagged, and how many weeks earlier, than the decks did.
Then run it beside the current QBR for one quarter and report the differences.
Target: flag material issues at least 6 weeks before they reach a QBR. This is achievable — if early
signals look weak, keep searching rawer sources before concluding.
```
- Prerequisites / plumbing: scheduled data refresh; a place to post alerts; owner who reviews them weekly.
- Outside judge: backtest hit rate and lead time on held-out quarters; leadership's own post-quarter review.
- Cost: multi-session project.

## 2. Engineering — slow page

**Original:** "Make the dashboard page load faster."

**Deepened (four-question pass):**
```
Target: dashboard p75 load under 200ms on a cold cache (currently ~10s). This is achievable.
Start from raw evidence, not intuition: record a Chrome performance trace and a server-side profile for a
cold load, and the slow query log from the DB. Build a flame graph and a waterfall; rank the top 5 costs
by measured milliseconds.
Fix in order of measured impact. After each change, re-run the same trace script and record the number.
Done = the trace script reports p75 < 200ms over 20 runs, and the existing test suite passes.
```

## 3. Content — weekly social posts

**Original:** "Write 5 posts for our X account this week."

**Altitude + Range:**
```
Goal: grow qualified followers (people who later click through to <product>) by <N>% this month.
Pull our last 90 days of posts with impressions, profile clicks, and link clicks. Find which hooks,
formats, and topics drove profile clicks — not likes — and test whether that holds for the most recent 30
days held out.
Workstreams: (1) data analysis as above, (2) find 3 live conversations in our niche worth joining with a
contrarian, sourced take, (3) red team: for each draft, the strongest reason a skeptical expert would
scroll past.
Deliver 5 posts, each tagged with the pattern it tests and the metric that will judge it next week.
```
