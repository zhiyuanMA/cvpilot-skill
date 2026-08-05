# Stage 4 · JD-Driven Technical Prep

> See [SKILL.md](../SKILL.md) § Core Principles and § Input Intake before executing this stage. Frameworks: [../frameworks/technical-depth-by-level.md](../frameworks/technical-depth-by-level.md), [../frameworks/technical-narrative-framework.md](../frameworks/technical-narrative-framework.md). Output HTML structure lives in [../frameworks/prep-report.md](../frameworks/prep-report.md).

**Goal:** generate a JD-specific, level-calibrated technical interview prep document, grounded in the candidate's real projects via the story bank — mining a broad foundation if the bank is still thin, and only targeted gaps once it isn't.

---

## Step 1 · Get the JD Signal and Target Level

Identify the job and get its technical Must-Haves, domain, and target level, per [SKILL.md](../SKILL.md) § Input Intake — this means finding the right `~/cvpilot-applications/<slug>/application.html` and reading its JD Decode section, not re-asking the user for the JD if it's already been decoded. If the level is ambiguous from the JD, **ask the user directly** rather than guessing — this determines the entire shape of what follows, per [../frameworks/technical-depth-by-level.md](../frameworks/technical-depth-by-level.md).

---

## Step 2 · Bank Maturity Check

Before doing gap analysis against this specific JD, check [../story-bank/_index.md](../story-bank/_index.md) for overall technical-bank maturity — not just JD-specific coverage:

- **Thin bank** (roughly fewer than 3 narratives, or missing coverage across more than half of the candidate's apparent technical domains) → recommend a **comprehensive** mining pass first, per [03-technical-mining.md](03-technical-mining.md)'s comprehensive mode, before narrowing to this JD's specific needs. Same reasoning as the behavioral track: a bank built one JD-domain at a time only ever covers what happened to overlap with jobs applied to so far.
- **Established bank** (reasonable domain coverage at or near the relevant levels already exists) → proceed directly to the JD-specific gap analysis below.

---

## Step 3 · JD-Specific Cross-Analysis

1. **JD technical Must-Haves → domain** — which technical domains does this role actually test?
2. **Bank narrative → domain + level_fit** — check [../story-bank/_index.md](../story-bank/_index.md): which required domains already have a narrative tagged at (or near) the target level? Which don't?

Where the JD wants a domain/level the bank still doesn't cover after Step 2, that's a targeted mining gap — offer to run [03-technical-mining.md](03-technical-mining.md) in targeted mode for the highest-priority gaps before generating the final prep document.

---

## Step 4 · Generate Level-Calibrated Questions

Using [../frameworks/technical-depth-by-level.md](../frameworks/technical-depth-by-level.md)'s question shapes for the target level, generate a set of technical questions across the JD's required domains. Don't default to generic system-design-interview questions — anchor every question in what this specific JD actually needs and what the candidate's background actually offers evidence for.

**Every question must carry four fields**, same discipline as behavioral prep:

1. **The question itself**, phrased at the right depth for the target level.
2. **What it tests** — the technical domain and the specific judgment being evaluated (e.g. "trade-off reasoning under scale constraints," not just "distributed systems").
3. **Why this role would ask it** — must point to a specific technical Must-Have from the JD decode.
4. **Which bank narrative answers it** — link to the specific narrative file, or mark `⚠️ Gap — needs a narrative mined`.

---

## Step 5 · Full Narrative Prep for Must-Practice Questions

Pick 3-5 questions that are most likely to come up and best-supported by the bank. Pull the full narrative directly from the bank entry, formatted per [../frameworks/technical-narrative-framework.md](../frameworks/technical-narrative-framework.md) (full form or short form, matching what's actually in the bank entry — don't inflate a short-form narrative into a full-form one that wasn't mined that way).

If a must-practice slot has no bank narrative yet, mine one first (Step 3) rather than leaving a generic placeholder.

---

## Step 6 · Gap List

List technical questions with no banked narrative behind them, or where the only available narrative doesn't really match the target level. Flag both cases plainly — a level mismatch is just as important to surface as a missing domain: "the closest narrative here is Intermediate-scoped; this role is asking Senior-level questions in this domain — worth mining something more senior-scoped, or being upfront in the interview about where you're stretching."

---

## Step 7 · Output

Write `technical-prep.html` into this job's folder (`~/cvpilot-applications/<slug>/`) per [../frameworks/prep-report.md](../frameworks/prep-report.md)'s structure: target level and reasoning → must-practice narratives (full form) → question list grouped by domain → gap list (including level mismatches). End with the standard disclaimer. In chat, summarize the must-practice set and flag the gap count, plus the file path.

---

## Common Snags

| Symptom | Handling |
|---|---|
| Bank has no technical narratives yet | This is what Step 2 is for — don't just patch this JD's gaps and move on. Recommend the comprehensive mining pass; it's the same conversational effort either way but produces a durable asset instead of a one-off. |
| Candidate's real experience sits below the JD's expected level | Don't paper over it. Flag it in the gap list as a level mismatch and let application-skill's match analysis, if it ran, inform whether this is worth pursuing at all. |
| Run standalone with no prior JD decode | Run a minimal condensed decode first (technical Must-Haves + level signal) — don't generate questions against raw JD text. |
