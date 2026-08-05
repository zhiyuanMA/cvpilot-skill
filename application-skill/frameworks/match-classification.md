# Match Classification — Rules and Scoring

This is the single source of truth for Stage 2 (`prompts/02-match-analysis.md`). The stage prompt executes this framework — it does not restate these rules.

Scoring must follow this framework exactly. Never assign a score by gut feel. Two people applying this framework to the same CV and JD should land on nearly the same result.

---

## 1. JD Requirement Verbatim-Fidelity Rule

Every `requirement` you classify must be an **exact substring of the JD text** — copied verbatim from Stage 1's decode output (which itself must have preserved verbatim JD quotes). Do not rephrase, normalize, re-capitalize, or correct grammar. Preserve original wording, casing, and punctuation exactly. If you cannot find an exact matching JD phrase for something you want to classify, do not include it.

---

## 2. Classification Definitions

Every JD requirement — every Must-Have and Nice-to-Have from Stage 1 — gets classified into exactly one of three buckets:

- **`match`** — The CV contains explicit, direct evidence that clearly satisfies the requirement.
- **`should_match`** — ALL of the following must be true:
  1. The JD explicitly requires this.
  2. The CV does **not** clearly or explicitly show it.
  3. The CV contains strong, directly related experience such that a reasonable recruiter would expect the candidate to possess this.
  4. If the candidate did **not** have this skill, it would be surprising given their background.
- **`gaps`** — The CV provides no clear or strong basis to believe the candidate meets this requirement. Do not infer or assume competence without strong supporting evidence.

**Mutual exclusivity**: each requirement appears in exactly one bucket. Classification priority when uncertain: `match` > `should_match` > `gaps`.

**Inference discipline**: never use `should_match` for weak correlations, "might have used X," general seniority without domain relevance, or tool/framework assumptions without a contextual signal in the CV. **If there is any reasonable doubt, classify as `gaps`, not `should_match`.**

---

## 3. Per-Item Score Mapping

Each classification maps to a numeric score for the aggregate formula below:

```
match        → 1.0  (full hit)
should_match → 0.5  (partial / adjacent)
gaps         → 0.0  (no hit)
```

A `match` additionally requires the CV evidence to be **specific and recent** (a concrete project or role, ideally within the last 3 years, with some quantified or verifiable detail) — a vague claim without specifics or a stale (5–10 year old) instance should be scored as `should_match` (0.5) even if the requirement is technically mentioned somewhere in the CV, since it doesn't rise to "explicit, direct evidence."

---

## 4. Aggregate Scoring Formula

```
Match Score = 0.6 × MustHaveScore + 0.2 × NiceToHaveScore + 0.2 × HiddenSignalFit

MustHaveScore    = Σ(score of each Must-Have item)   / number of Must-Have items
NiceToHaveScore  = Σ(score of each Nice-to-Have item) / number of Nice-to-Have items
```

**Hard caps** (a low individual score should not get diluted away by an otherwise-strong profile):

- Any Must-Have classified as `gaps` → total score capped at **≤75%**.
- Two or more Must-Haves classified as `gaps` → total score capped at **≤55%**.
- A "threshold" Must-Have (a hard gate — a required certification, clearance, or visa status) is missing → total score forced to **25–35%** regardless of everything else.

---

## 5. Hidden Signal Fit

Take the 3–5 strongest Hidden Signals identified in Stage 1. Score each 0 / 0.5 / 1 based on how the CV's overall profile aligns:

- CV/background clearly matches the signal → 1
- Neutral / can't tell either way → 0.5
- Clearly doesn't match / counter-signal → 0

```
HiddenSignalFit = Σ(signal scores) / number of signals scored
```

This stays a separate, more qualitative pass — Hidden Signals are about cultural/behavioral fit, not verifiable requirement evidence, so they don't go through the match/should_match/gaps machinery above.

---

## 6. Output as a Range, With Qualitative Bands

**Always give a range, never a single point estimate.** Reasonable width: ±5–8 percentage points (e.g. "72–80%"). This is because both requirement classification and Hidden Signal scoring involve judgment calls that would shift slightly under a different pass.

| Range | Band | Meaning |
|---|---|---|
| 85%+ | Direct fit | Interview-ready with little to no tailoring needed |
| 70–85% | Strong match | Tailoring (and a referral, if available) meaningfully improves interview odds |
| 55–70% | Moderate match | 1–2 clear gaps to address plus tailoring |
| 40–55% | Weak match | Applying is a judgment call based on opportunity cost |
| <40% | Not a match | Not recommended unless there's an unusual path in (strong referral, internal transfer) |

**Be conservative with high scores.** A real-world 80%+ is already a strong match. Inflated scores are the single biggest credibility killer for a tool like this.

---

## 7. Gap Three-Tier Taxonomy

Every item classified as `gaps` (and every `should_match` item worth calling out) gets a tier:

- **🔧 Fixable** (addressable within ~30 days) — the CV has adjacent experience that's just not surfaced or framed correctly; a missing certification/tool that's quick to obtain; or a portfolio case that can be extracted from existing project work.
- **⏳ Hard** (not fixable short-term) — missing years of experience in a specific domain, missing leadership experience that takes time to build, missing experience at a particular scale/stage, or a structural condition (degree, citizenship, visa).
- **🤷 Unimportant** (JD lists it, but it doesn't actually gate the decision) — a nice-to-have that isn't central to the role, boilerplate language repeated across most postings (e.g. generic "communication skills"), or something that overlaps with an already-covered Must-Have.

Drop 🤷 items from the user-facing gap list — including them only adds noise.

---

## 8. Risk vs. Gap

A **gap** is "what the CV is missing." A **risk** is "what a hiring manager would worry about even if nothing is technically missing." These are different things — a candidate can have almost no gaps and still carry significant risk (e.g. a 10-year Principal at a large company applying to a 40-person startup: few gaps, but real risk around culture fit, scope tolerance, and comp expectations).

Risk dimensions to check:

1. **Background span** — industry switch, company-size switch, role/discipline switch.
2. **Stability** — job-hopping frequency, short stints, employment gaps.
3. **Level span** — applying meaningfully above or below current level.
4. **Direction match** — past focus not fully aligned with what this JD needs.
5. **Compensation/expectations** — hiring manager may worry the candidate won't accept the likely offer.
6. **Visa / geography / timezone** — any hard constraint implied by the JD.

Every risk called out must include: **what a hiring manager would likely question**, and **how the candidate could respond** (ideally pointing to a specific kind of story they should have ready).

---

## 9. Recommendation Status

Translate the score, hard caps, and risk read into one of CVpilot's three verdicts:

- **`strong_candidate`** — no Must-Haves in `gaps`, band ≥70%, no unaddressed critical risk.
- **`needs_tailoring`** — band 40–70%, OR most Must-Have shortfalls sit in `should_match` (fixable through reframing), OR exactly one fixable Must-Have gap.
- **`not_recommended`** — band <40%, OR two or more Must-Haves in `gaps` (this mirrors the hard-cap trigger above), OR a non-fixable structural gap (visa, mandatory certification).

The recommendation must be consistent with the balance of match/should_match/gaps — never recommend `strong_candidate` when there are multiple critical gaps, and never soften a `not_recommended` verdict to spare feelings.

---

## 10. Consistency Checklist (verify before presenting output)

- No requirement appears in more than one of match/should_match/gaps.
- Every requirement classified is a literal, verbatim substring of the JD text.
- The recommendation status is consistent with the score band and hard-cap rules above.
- Tone is calm, professional, and decision-oriented — no scores presented as false precision, no fabricated requirements, no inflated scores to make the user feel better.
