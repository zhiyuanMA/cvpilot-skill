# Stage 3 · Tailored CV + Cover Letter

> See [SKILL.md](../SKILL.md) § Core Principles before executing this stage. Rules and formats live in [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md). Output persistence rules live in [../frameworks/application-report.md](../frameworks/application-report.md).

**Goal:** produce one tailored CV rewrite (not multiple variants) and a role-specific cover letter, grounded entirely in Stage 2's match analysis. Runs only on user confirmation — never automatically.

**The single most important rule here (from [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md) §1): never fabricate.** Every rewrite reorganizes, reframes, and re-quantifies real facts already in the CV. It never invents a new achievement, number, or responsibility, and never upgrades a verb beyond what actually happened (e.g. "contributed to" does not become "led").

---

## Step 1 · Gather Inputs

1. Stage 2's match analysis — specifically the `match` and `should_match` items with their evidence.
2. The candidate's full CV text.
3. The JD (from Stage 1).

---

## Step 2 · Build the Tailoring Plan First

Before rewriting anything, build a tailoring plan covering **`should_match` items only — never `gaps`.** This is a deliberate constraint: tailoring re-surfaces experience the candidate plausibly already has; it does not manufacture experience they don't.

One row per `should_match` item:

```
Target requirement: "experience with Kubernetes" (verbatim JD quote)
Existing experience: deep containerized-deployment work (Docker, ECS), on-call
  ownership of production services
Suggested change: reframe the "Infrastructure" bullet in the [Company] role to
  name the orchestration/deployment work explicitly, and confirm with the
  candidate whether Kubernetes specifically was used anywhere, even briefly
CV section: Experience → [Company] → Infrastructure bullet
```

Show this plan to the user before producing the full rewrite — it's the checkpoint where they can say "actually I don't want to emphasize that" before you've written the whole document.

---

## Step 3 · Decide Reordering and Emphasis

For `match` items too (not just `should_match`), decide what should move up, get emphasized, or get trimmed — most relevant and most recent experience first, per [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md) §2.

---

## Step 4 · Produce the Tailored CV

Write the full tailored CV following [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md) §2's merged ATS + hiring-manager-readable requirements (standard sections, no tables/columns/images, JD keyword coverage, problem→judgment→action→result bullets, Hidden-Signal-aligned language where the underlying fact supports it, 1–2 preserved hook details per key role).

---

## Step 5 · Show the Diff

For every bullet you added, cut, or meaningfully changed, show original → tailored + which JD requirement or Hidden Signal it aligns to, per [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md) §3's format. Don't just hand over the final document — the diff is what lets the user learn the pattern and trust the changes.

---

## Step 6 · Cover Letter

Write a cover letter as a professional career writer would: concise, role-specific, 200–300 words, aligning the candidate's real experience to the JD's requirements. Build it from, in this order: the CV, the JD, Stage 1's decode, Stage 2's match analysis, and this stage's tailoring plan. Follow [../frameworks/resume-tailoring.md](../frameworks/resume-tailoring.md) §4's checklist.

---

## Step 7 · Update the Job Folder

Update `~/cvpilot-applications/<slug>/application.html` (already holding the Stage 1 and Stage 2 sections) with the Tailored CV section (including the diff list from Step 5) and the Cover Letter section, and bump status to `tailored`. In chat, give a summary of what changed and why, plus the cover letter in full (it's short enough to be useful inline) and the file path — not the full tailored CV inline, since it's now saved.

---

## Step 8 · Offer interview-prep-skill

Mention that interview-prep-skill (behavioral and technical interview prep) is available next, per [SKILL.md](../SKILL.md) § Flow Control — don't run it automatically. Note that it will read the tailored CV and cover letter just saved to this job's folder, not the original CV, since that's what the interviewer will actually have seen.

---

## Common Snags

| Symptom | Handling |
|---|---|
| CV is missing a number for a claim worth quantifying | Don't invent one. Ask: "This would land harder with a number — do you have one, or a conservative estimate?" |
| User wants to exaggerate | Push back directly: exaggeration that can't be backed up in an interview backfires — every line on a tailored CV gets followed up on. |
| CV/JD gap is too large to tailor meaningfully | Don't force it — point back to Stage 2's verdict. If it was `not_recommended`, tailoring isn't the right next step. |
| User only wants the CV or only the cover letter | Produce just the one requested; mention the other is available. |
