# Stage 2 · Evidence-Based Match Analysis

> See [SKILL.md](../SKILL.md) § Core Principles before executing this stage. All classification rules and the scoring formula live in [../frameworks/match-classification.md](../frameworks/match-classification.md) — this file executes that framework, it does not restate it. Output persistence rules live in [../frameworks/application-report.md](../frameworks/application-report.md).

**Goal:** produce a rigorous, evidence-based comparison of the candidate's CV against the JD's requirements — not a gut-feel score. Fixed output: match score, strengths, gaps, risk, and a recommendation.

**Never classify or score without Stage 1's decode output.** Matching against raw JD text instead of the decoded Must-Haves/Nice-to-Haves/Hidden Signals means aligning to recruiting-speak, not to what's actually being asked for.

---

## Step 1 · Gather Inputs

1. Stage 1's Must-Have and Nice-to-Have list, with verbatim JD quotes.
2. Stage 1's Hidden Signals.
3. The candidate's **full** CV text — not a summary.

If the CV is too short to say anything meaningful (a LinkedIn headline, a couple of lines), stop and ask for a fuller version before scoring. Don't score a thin CV just because it was given.

---

## Step 2 · Classify Every Requirement

For every Must-Have and Nice-to-Have from Stage 1, classify it as `match`, `should_match`, or `gaps` following [../frameworks/match-classification.md](../frameworks/match-classification.md) §1–§2 exactly. This is the core discipline of this stage — apply it strictly:

- The `requirement` string must be the exact verbatim JD quote from Stage 1 — never paraphrase it.
- `match` requires explicit, direct CV evidence — capture the specific CV evidence alongside it.
- `should_match` requires ALL of: the JD explicitly requires it; the CV doesn't clearly show it; the CV has strong, directly related adjacent experience; it would be surprising if the candidate didn't have it. Capture the inferred experience and why it isn't clearly shown.
- `gaps` is the default when evidence is missing or too weak to justify `should_match` — capture the reason. **When in doubt, this is the bucket.**
- Never let the same requirement appear in more than one bucket.

Present the result as three lists, e.g.:

```
match:
- "3+ years of experience with distributed systems" — CV evidence: led the migration
  of [Company]'s order service to a distributed architecture, 2022–2023, handling 50k+
  requests/min.

should_match:
- "experience with Kubernetes" — inferred from: CV shows deep containerized-deployment
  experience (Docker, ECS) and production on-call ownership; Kubernetes itself isn't
  named. Why not clear: no explicit Kubernetes mention anywhere in the CV.

gaps:
- "experience in a regulated industry (finance/healthcare)" — reason: CV is entirely
  consumer tech and gaming; no adjacent regulated-industry signal anywhere.
```

---

## Step 3 · Score

Apply [../frameworks/match-classification.md](../frameworks/match-classification.md) §3–§6: map each classification to a score, compute `MustHaveScore` and `NiceToHaveScore`, score `HiddenSignalFit` separately, apply the weighted formula and hard caps, and present the result as a range with a qualitative band — never a single-point score.

```
Match score: 72–80% (Strong match, with two gaps worth addressing)
Weighting: 60% Must-Have + 20% Nice-to-Have + 20% Hidden Signal fit
```

---

## Step 4 · Gaps

Tier every gap per [../frameworks/match-classification.md](../frameworks/match-classification.md) §7 (🔧 fixable / ⏳ hard / 🤷 unimportant). Drop 🤷 items from what you show the user — listing them only adds noise.

---

## Step 5 · Risk

Apply [../frameworks/match-classification.md](../frameworks/match-classification.md) §8. For each risk dimension that applies, give: the risk itself, what a hiring manager would likely question, and how the candidate could respond (ideally pointing toward the kind of story — see interview-prep-skill — that would address it).

---

## Step 6 · Recommendation

Apply [../frameworks/match-classification.md](../frameworks/match-classification.md) §9 to land on `strong_candidate` / `needs_tailoring` / `not_recommended`, with reasoning under 100 words. The reasoning must be consistent with the balance of match/should_match/gaps — don't soften a weak verdict.

---

## Step 7 · Consistency Check

Before presenting anything, run through [../frameworks/match-classification.md](../frameworks/match-classification.md) §10: no duplicated requirements, every requirement is a verbatim JD substring, recommendation matches the score band, tone is calm and decision-oriented, no inflated scores.

---

## Step 8 · Update the Job Folder

Update `~/cvpilot-applications/<slug>/application.html` (created in Stage 1) with the Match Analysis section — the full match/should_match/gaps breakdown, score, gap tiers, risk read, and recommendation — and bump status to `matched`. **Do this regardless of the verdict, including `not_recommended`** — per [../frameworks/application-report.md](../frameworks/application-report.md) §3, a record of why a job wasn't pursued still has value. In chat, give a summary — score, top 2-3 strengths, top 2-3 gaps, recommendation — and the file path, not the full breakdown inline.

---

## Step 9 · Gate on the Recommendation

Follow [SKILL.md](../SKILL.md) § Flow Control exactly: offer Stage 3 for `strong_candidate` and `needs_tailoring`; explain the verdict for `not_recommended` without auto-offering Stage 3. Always mention that interview-prep-skill (behavioral and technical interview prep) is available regardless of verdict.

---

## Common Snags

| Symptom | Handling |
|---|---|
| CV is thin or unrelated to the JD | Don't inflate the score to soften the message. State the low score plainly, along with what would be needed to close the gap. |
| User wants to hear a higher score | Stay objective. A low score with a concrete path forward is more useful than a flattering score that leads to a rejection later. |
| Stage 1 hasn't run yet | Run a minimal version of Stage 1 first (at least Must-Haves + Hidden Signals) before scoring — never skip straight to matching. |
| CV and JD are in completely different domains | Say so directly: "this match is too low (<40%) to be worth tailoring effort — worth reconsidering whether this is the right application to pursue." |
