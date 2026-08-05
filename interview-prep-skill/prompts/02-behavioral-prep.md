# Stage 2 · JD-Driven Behavioral Prep

> See [SKILL.md](../SKILL.md) § Core Principles and § Input Intake before executing this stage. Frameworks: [../frameworks/star-framework.md](../frameworks/star-framework.md), [../frameworks/competency-tags.md](../frameworks/competency-tags.md), [../frameworks/company-profiles.md](../frameworks/company-profiles.md). Output HTML structure lives in [../frameworks/prep-report.md](../frameworks/prep-report.md).

**Goal:** generate a JD-specific behavioral interview prep document — Top 20 questions plus full STAR templates for the Top 5 — by cross-referencing the target JD against the persistent story bank, mining a broad foundation if the bank is still thin and only targeted gaps once it isn't.

---

## Step 1 · Get the JD Signal

Identify the job and get its Must-Haves and Hidden Signals, per [SKILL.md](../SKILL.md) § Input Intake — this means finding the right `~/cvpilot-applications/<slug>/application.html` and reading its JD Decode section, not re-asking the user for the JD if it's already been decoded.

---

## Step 2 · Bank Maturity Check

Before doing gap analysis against this specific JD, check [../story-bank/_index.md](../story-bank/_index.md) for overall bank maturity — not just JD-specific coverage:

- **Thin bank** (roughly fewer than 4-5 stories, or covering fewer than half of the 12 core competencies in [../frameworks/competency-tags.md](../frameworks/competency-tags.md)) → recommend a **comprehensive** mining pass first, per [01-story-mining.md](01-story-mining.md)'s comprehensive mode, before narrowing to this JD's specific needs. Explain why: a bank built one JD-gap at a time only ever covers what happened to overlap with jobs applied to so far — a broader pass now saves much more mining time across every future application than a narrow one saves right now. This is especially worth doing on a candidate's first run of this skill.
- **Established bank** (reasonable baseline coverage already exists) → proceed directly to the JD-specific gap analysis below; no need to re-mine ground that's already solid.

---

## Step 3 · JD-Specific Cross-Analysis

Build two mappings:

1. **JD dimension → competency tag** — which competencies (from [../frameworks/competency-tags.md](../frameworks/competency-tags.md)) does this role clearly test, based on the Must-Haves and Hidden Signals?
2. **Bank story → competency tag** — check [../story-bank/_index.md](../story-bank/_index.md): which of the required competencies already have a strong, banked story? Which don't?

Where the JD wants a competency the bank still doesn't cover after Step 2, that's a targeted mining gap — offer to run [01-story-mining.md](01-story-mining.md) in targeted mode for those specific gaps before generating the final prep document. Don't re-mine competencies the bank already covers well.

---

## Step 4 · Generate the Top 20 Questions

Across four weighted categories (adjust the split based on what the JD emphasizes):

| Category | Approx. count | Notes |
|---|---|---|
| General behavioral | ~8 | Core dimensions: Ownership, Conflict, Failure, Ambiguity, Influence, etc. |
| Company-values-specific | ~5 | Directly targets this company's Hidden Signals/values (see [../frameworks/company-profiles.md](../frameworks/company-profiles.md)) |
| Role/craft-specific | ~5 | Domain competence framed as a behavioral question |
| Level/stage-specific | ~2 | Targets the level and team stage from the JD decode |

**Every question must carry four fields:**

1. **The question itself.**
2. **What it tests** — the competency tag(s).
3. **Why this company would ask it** — must point to a specific Must-Have or Hidden Signal from the decode.
4. **Which bank story answers it** — link to the specific story file, or mark `⚠️ Gap — needs a story mined` if the bank has nothing suitable.

---

## Step 5 · Full STAR for the Top 5

Pick the 5 questions that are (a) most likely to actually be asked at this company, (b) backed by a strong banked story, and (c) reusable across the widest range of other questions (see [../frameworks/star-framework.md](../frameworks/star-framework.md)'s "one story, many questions").

Pull the full STAR content directly from the bank story file — don't re-derive it. If a Top 5 slot doesn't have a banked story yet, mine one first (Step 3) rather than leaving a placeholder.

---

## Step 6 · Gap List

List Top 20 questions with no banked story behind them. Flag them plainly: "no story banked for this one — worth mining before the interview." Point to [01-story-mining.md](01-story-mining.md).

---

## Step 7 · Company Flavoring

If the user names a target company covered in [../frameworks/company-profiles.md](../frameworks/company-profiles.md), angle the question wording and story emphasis toward that company's style.

---

## Step 8 · Output

Write `behavioral-prep.html` into this job's folder (`~/cvpilot-applications/<slug>/`) per [../frameworks/prep-report.md](../frameworks/prep-report.md)'s structure: Top 5 (full STAR) → Top 20 table (grouped by category) → gap list. End with the standard disclaimer. In chat, summarize the Top 5 and flag the gap count, plus the file path.

---

## Common Snags

| Symptom | Handling |
|---|---|
| Bank is thin or empty | This is what Step 2 is for — don't just patch this JD's gaps and move on. Recommend the comprehensive mining pass, since it's the same conversational effort either way but produces a durable asset instead of a one-off. |
| User wants to skip straight to the Top 20 without mining anything | Respect it, but be upfront: most questions will land in the gap list, and offer the comprehensive pass again before wrapping up. |
| Run standalone with no prior JD decode | Run a minimal condensed decode first (Must-Haves + Hidden Signals) — don't generate questions against raw JD text. |
