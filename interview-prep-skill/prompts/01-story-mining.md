# Stage 1 · Behavioral Story Mining

> See [SKILL.md](../SKILL.md) § Core Principles before executing this stage.

**Goal:** turn a candidate's real work history into interview-ready STAR stories, saved to the persistent story bank so they never have to be re-derived from scratch for the next application. This is a conversation, not a questionnaire — one question at a time.

**Bank first, always.** Before mining anything new, check [../story-bank/_index.md](../story-bank/_index.md) for a story that already covers what you're after.

**Two ways this stage gets triggered — both are normal:**

- **Comprehensive** — the user asks directly ("help me build my story bank," "let's prep some stories") or the bank is thin (see [02-behavioral-prep.md](02-behavioral-prep.md)'s bank maturity check). Run the full four-quadrant scan below across the candidate's broader experience, not narrowed to any one JD. This is the mode that actually makes the bank valuable — a bank built one JD-specific gap at a time never accumulates broad coverage, because most of what a candidate has to offer doesn't happen to overlap with the first few jobs they run through this skill. Treat comprehensive mining as a one-time-ish investment that pays off on every future application, and default to it whenever the bank is thin, even if the immediate trigger was a specific JD.
- **Targeted** — [02-behavioral-prep.md](02-behavioral-prep.md) sends you here for one specific missing competency because the bank is otherwise already solid. In that case, skip straight to the relevant quadrant/competency rather than running the full scan — re-mining ground that's already well covered wastes the user's time.

If you're not sure which mode applies, ask: "Want to do a broader pass to build out your story bank, or just fill in the one or two gaps for this application?"

---

## Layer 1 · Icebreaker

Many candidates start with "I don't have anything impressive to talk about." Two techniques to get past that:

**(A) Counterfactual questioning** — "If you hadn't pushed for that, or hadn't done it, what would have gone worse?" This surfaces impact the candidate has stopped noticing because it's just "what they do."

**(B) Four-quadrant timeline scan** — walk through one quadrant at a time, not all at once:
- **Project** — something they built, shipped, or drove that they're proud of
- **Conflict** — a disagreement with a coworker, manager, or stakeholder
- **Failure** — a mistake, missed deadline, or wrong call (these are valuable — interviewers want to see reflection, not a flawless record)
- **Leadership / Initiative** — a time they stepped up without being asked to

Ask about one quadrant, let them respond, then move to the next. Don't fire off all four at once.

---

## Layer 2 · Deep-Dig

Once a candidate has a rough story, fill in the full STAR — this is where most of the real work happens. Two elements people skip most often, and where to push:

- **T (Task)** — what was *specifically theirs*, not the team's. Whenever the candidate says "we decided" or "we built," redirect: **"What part of that was specifically yours?"** This is the single most important discipline in this stage.
- **R (Result)** — quantified outcome. If they don't have a number offhand, ask directly rather than letting the story stay vague: "Do you have a rough number for that — even an estimate?" Never write one in yourself.

Probe Action for the actual judgment call, not just a list of steps: "What made you choose that approach over the alternative?" / "What was the hardest part of that?"

---

## Layer 3 · Tagging

Once the story is structured:

1. Map it to competency tags using [../frameworks/competency-tags.md](../frameworks/competency-tags.md) — **one primary tag, one or two secondary.** Don't over-tag.
2. If the candidate has named a target company, tag `company_fit` using [../frameworks/company-profiles.md](../frameworks/company-profiles.md) (e.g. `Amazon-LP:Ownership`).
3. Note which other questions this same story could plausibly answer (see [../frameworks/star-framework.md](../frameworks/star-framework.md)'s "one story, many questions") — this is the direct payoff of banking a story instead of mining fresh ones every time.

---

## Layer 4 · Save to Bank

1. Write the story to `../story-bank/<slug>.md` using [../story-bank/_story-template.md](../story-bank/_story-template.md).
2. Update [../story-bank/_index.md](../story-bank/_index.md) — add it to the competency table and the "all entries" table.
3. Confirm with the user: "Saved. This should also work for questions about [X, Y] — want to mine another one, or move on?"

---

## Stuck? Troubleshooting

| Symptom | Handling |
|---|---|
| User keeps saying "we" | Redirect: "What part of that was specifically yours?" Don't let a team story stand in for a personal one. |
| No numbers at all | Fall back to qualitative evidence (scope, visibility, who noticed) and mark `metrics: not yet confirmed` in the template rather than inventing a number. |
| User insists they have nothing worth mining | Use the counterfactual technique (Layer 1A) — it usually surfaces something they'd stopped seeing as notable. |
| Story is really about someone else's decision | Probe for the candidate's actual contribution before continuing — if there genuinely isn't one, this isn't a usable story for them. |
