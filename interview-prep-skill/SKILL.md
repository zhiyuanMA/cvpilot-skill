---
name: interview-prep-skill
description: "Behavioral and technical interview preparation grounded in a candidate's real work history, cross-referenced against a specific job's requirements. Maintains a persistent, reusable story bank (behavioral STAR stories and technical decision narratives) so a candidate mines their real experience once and reuses it across every future application, instead of re-deriving similar content for every job. Two tracks: (1) behavioral prep — mines STAR stories through a guided one-question-at-a-time conversation (icebreaker, deep-dig on personal ownership and quantified results, competency tagging), then generates a JD-specific Top 20 behavioral questions with a full STAR template for the Top 5 must-practice; (2) technical prep — mines technical decision narratives (context, options considered, trade-offs, outcome, reflection) from real projects through guided probing, calibrated to the target seniority level (Junior/Intermediate/Senior/Staff) inferred from the JD, then generates level-appropriate technical questions grounded in those narratives. Never fabricates a story or a number — everything comes from the candidate's own account, confirmed with them. Part of the cvpilot-skill toolkit; reads the same per-job folder under ~/cvpilot-applications/ that application-skill wrote, grounding prep in the actual tailored CV and cover letter that was submitted (not just the original CV), since that's what the interviewer will have seen. Trigger phrases: behavioral interview, BQ prep, STAR method, tell me about a time, interview questions, mock interview, story bank, technical interview, system design interview, technical deep dive, interview prep, mine my stories, Amazon leadership principles, competency questions."
---

# Interview Prep Skill

Turns a candidate's real work history into interview-ready behavioral and technical prep, cross-referenced against a specific job. Unlike application-skill, this skill **persists** — the story bank it builds is meant to be reused across every future application, not just this one.

## Two Tracks

```
Behavioral track                          Technical track
      │                                          │
      ▼                                          ▼
Stage 1 · Story mining  ───► story-bank/   Stage 3 · Technical mining  ───► story-bank/
      │  (comprehensive on a thin bank,          │  (comprehensive on a thin bank,
      │   targeted once established)             │   targeted once established)
      ▼                                          ▼
Stage 2 · Behavioral prep  ─► behavioral-prep.html  Stage 4 · Technical prep  ─► technical-prep.html
   (Top 20 + Top 5 STAR,                      (level-calibrated questions +
    JD-cross-referenced)                       must-practice narratives)
```

Both tracks follow the same shape: **check the bank first.** What happens next depends on how mature the bank already is, not just on this one JD:

- **Bank is thin or empty** (typically a candidate's first run) → mine comprehensively across the candidate's broader experience — all four behavioral quadrants, all apparent technical domains — not narrowed to just what this JD happens to test. A bank built one JD-gap at a time never accumulates real breadth, since most of what a candidate has to offer won't overlap with the first few jobs they run through this skill. This is a deliberate one-time-ish investment: the same conversational effort produces a durable, reusable asset instead of a one-off.
- **Bank already has solid baseline coverage** → mine only the specific gaps this JD's requirements expose. Re-mining ground that's already well covered wastes the user's time.

Stage 2 and Stage 4 each start with an explicit bank-maturity check (see their prompt files) to decide which mode applies. Run one track, the other, or both — ask the user which they want if it's not obvious from how they asked. A user can also trigger comprehensive mining directly at any time ("help me build my story bank") without going through a JD-driven prep flow at all.

## Input Intake

**Which job.** application-skill and this skill share one fixed root, `~/cvpilot-applications/`, one folder per job (see [../application-skill/frameworks/application-report.md](../application-skill/frameworks/application-report.md) for the naming convention). Figuring out which job to prep for:
- If application-skill just ran in this conversation, use that job's folder directly — no need to ask.
- Otherwise, list the subfolders under `~/cvpilot-applications/` and ask the user which one (folder names encode company + role + date, so this is usually a quick pick).
- If the user wants prep for a job that was never run through application-skill at all, that's fine — gather the JD and CV fresh (see below) and create a new folder for it the same way application-skill would.

**JD signal and CV, once the job is identified — read `~/cvpilot-applications/<slug>/application.html`:**
- **JD signal** (Must-Haves, Hidden Signals, target level) comes from that file's JD Decode section.
- **CV** — this is the important part: if the file's status is `tailored` (Stage 3 ran), use the **Tailored CV** section as the candidate's CV, not their original one. That's the version the interviewer will actually have read. If status is only `decoded` or `matched` (Stage 3 never ran), fall back to asking the user for their CV directly, same mechanics as application-skill (local file path via `Read`, or pasted text) — and note in your output that prep is based on the original CV since no tailored version exists for this job.
- If no `application.html` exists at all for this job yet (fresh gather case above), get the JD and CV the same way application-skill does — Seek/LinkedIn URL via `WebFetch` with a paste fallback, or pasted text, never guessing JD content from a company name — then run a **condensed decode**: just Must-Haves, Hidden Signals, and a level/title read, using [../application-skill/frameworks/decode-patterns.md](../application-skill/frameworks/decode-patterns.md). Don't run the full 5-layer treatment — that's application-skill's job.
- If the target level is genuinely ambiguous, ask the user directly rather than guessing (this matters a lot for the technical track — see [frameworks/technical-depth-by-level.md](frameworks/technical-depth-by-level.md)).

## Core Principles

1. **Bank first, always.** Before mining anything new, check [story-bank/_index.md](story-bank/_index.md) for a story or narrative that already covers what's needed. On a thin bank, default to comprehensive mining (broad coverage of the candidate's experience) rather than narrowly patching just this JD's gaps — see § Two Tracks. Once the bank has solid baseline coverage, mining should stay targeted at genuine gaps.
2. **One question at a time.** Mining is a conversation, never a questionnaire — don't fire off multiple probing questions in one message.
3. **Never fabricate.** Every story and technical narrative comes from the candidate's real account. Numbers are confirmed with them, never estimated or invented on their behalf.
4. **Redirect "we" to "I."** Whenever a candidate describes a team decision, push for their specific personal contribution before accepting the story as usable.
5. **Calibrate technical depth to the target level.** Don't force a Junior-scoped project into a fabricated system-design narrative, and don't let a Senior/Staff candidate settle for implementation-level answers that undersell their actual scope. See [frameworks/technical-depth-by-level.md](frameworks/technical-depth-by-level.md).
6. **Standard disclaimer.** Every generated prep document ends with: *"This content is generated by AI for reference only. Please review and adjust before use."*

## Output

- **Story bank** (`story-bank/*.md`) persists across sessions and applications — this is the entire point of the mining engines. It lives inside this skill's own directory, stays plain Markdown (these are working records meant to be read/edited directly, not polished documents), and isn't tied to any single job application, unlike everything else below.
- **Prep documents** (`behavioral-prep.html`, `technical-prep.html`) are per-application deliverables, written as HTML **into the same job folder** application-skill uses: `~/cvpilot-applications/<company-slug>-<role-slug>-<YYYYMMDD>/`. Structure and styling live in [frameworks/prep-report.md](frameworks/prep-report.md) — it shares the exact same CSS as application-skill's `application.html`, so everything in a job's folder reads as one coherent toolkit.
- Give a concise chat summary after generating a prep document, plus the file path — the full detail lives in the file.

## Reference Files

Load these on demand — don't read the whole skill directory upfront.

**Prompts:**
- [prompts/01-story-mining.md](prompts/01-story-mining.md) — behavioral mining engine
- [prompts/02-behavioral-prep.md](prompts/02-behavioral-prep.md) — JD-driven behavioral prep (Top 20 + Top 5 STAR)
- [prompts/03-technical-mining.md](prompts/03-technical-mining.md) — technical mining engine
- [prompts/04-technical-prep.md](prompts/04-technical-prep.md) — JD-driven, level-calibrated technical prep

**Frameworks:**
- [frameworks/star-framework.md](frameworks/star-framework.md) — STAR/CAR/SOAR structure, used by Stage 1/2
- [frameworks/competency-tags.md](frameworks/competency-tags.md) — behavioral competency dictionary, used by Stage 1/2
- [frameworks/company-profiles.md](frameworks/company-profiles.md) — company interview-style notes, used by Stage 2
- [frameworks/technical-narrative-framework.md](frameworks/technical-narrative-framework.md) — technical decision-narrative structure, used by Stage 3/4
- [frameworks/technical-depth-by-level.md](frameworks/technical-depth-by-level.md) — what "good" looks like at each level, used by Stage 3/4
- [frameworks/prep-report.md](frameworks/prep-report.md) — HTML structure/styling for the prep documents, used by Stage 2/4

**Story bank:**
- [story-bank/_index.md](story-bank/_index.md) — reverse-lookup index, check before every mining session
- [story-bank/_story-template.md](story-bank/_story-template.md) — behavioral story template
- [story-bank/_technical-template.md](story-bank/_technical-template.md) — technical narrative template
