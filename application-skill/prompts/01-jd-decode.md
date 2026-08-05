# Stage 1 · JD Decode

> See [SKILL.md](../SKILL.md) § Core Principles and § Input Intake before executing this stage. Output persistence rules (fixed directory, folder naming, HTML structure) live in [../frameworks/application-report.md](../frameworks/application-report.md).

**Goal:** turn a job posting written in recruiting-speak into a structured picture of what the hiring manager actually wants. Every later stage depends on this stage's output — always run it first.

---

## Step 1 · Gather Inputs

Get from the user (following SKILL.md's Input Intake mechanics):

1. **Full JD text** (required). Try the URL first if given; fall back to asking for pasted text if the fetch fails.
2. **Company name + role + level** (required — ask if not obvious from the JD itself).
3. **Target level** (optional). If the level the user is interviewing for differs from what the JD states, it changes how the Must-Haves should be read.

**Don't guess when you don't have the full JD text.** A summary isn't enough — Hidden Signals are usually buried in specific word choice, ordering, and phrasing that a summary strips out.

---

## Step 2 · Five-Layer Breakdown

Produce all five layers, in order — don't skip one.

### Layer 1 · What the hiring manager actually wants (the most valuable layer)

Translate the JD's marketing language back into the hiring manager's real expectations:

- For each JD requirement, ask: "the literal ask is ___, but the person the hiring manager actually wants is ___." These are often different.
- Separate genuine hard requirements from packaging — "strong experience with X" often really means "done X once or twice, that's enough."
- Use [../frameworks/decode-patterns.md](../frameworks/decode-patterns.md)'s translation table.

Output format:

```
JD says:
> "Looking for a Product Designer with strong AI experience"

What the hiring manager is actually looking for:
- Has shipped an AI product (ideally at least one end-to-end)
- Can move fast with PMs and engineers
- Can define a 0-to-1 product shape

Not required:
- Doesn't need to train models or write prompt-eval pipelines
```

3–5 translations like this is enough — pick the most important requirements in the JD.

### Layer 2 · Must-Haves (disqualifying if missing)

3–5 items. Each must be **verifiable** (visible on a CV, or askable in an interview) — not a vague buzzword.

**Every Must-Have must carry the exact JD phrase it's drawn from, quoted verbatim**, alongside the interpretation and a one-line reason it's a Must-Have (not just Nice-to-Have):

```
- Must-Have: "3+ years of experience with distributed systems" (verbatim JD quote)
  Real ask: shipped and operated a distributed system in production, not just studied the theory
  Why must-have: appears twice in the JD, explicitly flagged "required"
```

This verbatim quote is required — Stage 2 cannot classify requirements accurately without the literal JD phrase, not a paraphrase.

### Layer 3 · Nice-to-Haves (bonus, not disqualifying)

3–5 items, same verbatim-quote format as Layer 2. Missing these doesn't disqualify a candidate; having them is a clear plus.

### Layer 4 · Hidden Signals (unstated culture/fit expectations)

What the JD's word choice reveals about the kind of person the hiring manager wants — the layer most often skipped and most often what actually differentiates a strong application.

Use [../frameworks/decode-patterns.md](../frameworks/decode-patterns.md)'s Hidden Signal dictionary. Output format:

```
JD repeatedly uses "ambiguity" + "ownership" + "drive"
→ Signal: this company is looking for a self-driven person, not someone who waits for a spec.
→ Both the CV and interview answers should emphasize proactively defining problems and driving decisions.
```

3–5 of the strongest signals is enough.

### Layer 5 · Level, Team, and Stage

Infer the real shape of the role:

- **Level**: the stated title vs. what the responsibilities actually imply (these often differ).
- **Team size**: solo? small team (<5)? larger group (10+)? Only state this if the JD gives a signal — otherwise say so.
- **Team stage**: 0-to-1 / 1-to-N / mature / transforming.
- **Reporting line**: who does this role report to, if stated?
- **Likely pain point**: why is this role open now (growth, backfill, new direction)?

Label every inference with what it's based on. If the JD doesn't say, write "not stated in the JD" — never present a guess as fact.

---

## Step 3 · Create the Job Folder and Persist

Per [../frameworks/application-report.md](../frameworks/application-report.md) §2: determine the folder slug from company + role (auto-generated), or ask the user for a label if the company isn't disclosed. Check whether `~/cvpilot-applications/<slug>/` already exists — if it's genuinely the same job, update the existing `application.html`; otherwise create the folder fresh.

Write `application.html` with the header and the JD Decode section (all five layers), status `decoded`, per the framework's HTML structure. In chat, give a short summary (company/role, the strongest 2-3 signals) and the file path — not the full five-layer breakdown inline, since it's now saved.

## Step 4 · Hand Off

Move directly into Stage 2 (per SKILL.md's Flow Control) unless the user explicitly asked for only the decode.

---

## Common Snags

| Symptom | Handling |
|---|---|
| JD is very short / mostly buzzwords | Say so directly: "this JD doesn't have much to work with — I can extract limited signal from it. It'd help to also share: recent product direction, the hiring manager's LinkedIn, or other team members' backgrounds." |
| User only gave a link and it couldn't be fetched | Ask them to paste the JD text. **Never guess JD content from the company name.** |
| User asks "should I even apply?" | Don't answer that here — that's what Stage 2's recommendation gate is for. Note it and continue the decode. |
