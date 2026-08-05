---
name: application-skill
description: "Turns a Seek NZ/AU (or LinkedIn) job posting and a candidate's CV into a complete, evidence-based application package, persisted to a per-job folder under ~/cvpilot-applications/: (1) a 5-layer JD decode that reveals what the hiring manager actually wants versus recruiting-speak, plus Must-Have / Nice-to-Have / Hidden-Signal breakdown and level, team, and stage inference; (2) a strict, evidence-based match analysis that classifies every JD requirement as match, should_match, or gaps against the CV using verbatim JD quoting, converts that classification into a weighted numeric match score that is hard-capped when Must-Haves are missing, and adds a 3-tier gap taxonomy plus a hiring-manager risk read; (3) an actual tailored CV rewrite — never fabricated, only reorganized, highlighted, and quantified from real facts — plus a 200-300 word role-specific cover letter. Three linear stages, each progressively updating one HTML file per job so the record (including jobs you decided not to pursue) survives past this conversation. Part of the cvpilot-skill toolkit; interview-prep-skill later reads this same per-job folder — including the actual tailored CV and cover letter that was submitted — to ground interview preparation in what the interviewer will have actually seen. Trigger phrases: job description, JD, Seek job, Seek NZ, Seek AU, LinkedIn job posting, should I apply, match score, resume match, CV match, gap analysis, tailor my resume, tailor my CV, rewrite my resume, cover letter, job search, career coach, application strategy."
---

# Application Skill

Turns a job posting and a CV into a decoded JD, a rigorous match analysis, and a tailored CV + cover letter. Three stages, persisted progressively to a per-job folder so the result survives past this conversation and interview-prep-skill can read it back later.

## Pipeline

```
JD + CV in hand
      │
      ▼
Stage 1 · Decode the JD  ──────────────────────────►  01-jd-decode.md
      │  (runs automatically into Stage 2)
      ▼
Stage 2 · Evidence-based match analysis  ──────────►  02-match-analysis.md
      │  (gate on recommendation status — see Flow Control)
      ▼
Stage 3 · Tailored CV + cover letter  ─────────────►  03-tailor-and-cover-letter.md
         (only on user confirmation)
         └─► hand off to interview-prep-skill for behavioral/technical interview prep
```

## Input Intake

Read this once — every stage prompt assumes these mechanics rather than restating them.

**Job description:**
- A Seek (`seek.co.nz`, `seek.com.au`) or LinkedIn (`linkedin.com/jobs/`) URL → use `WebFetch` and ask it to extract the full job description: title, company, responsibilities, requirements, nice-to-haves, culture/team description. LinkedIn frequently sits behind a login wall and Seek pages can also fail to fetch cleanly.
- If the fetch fails, returns clearly incomplete content, or is blocked → tell the user plainly that the page could not be fetched, and ask them to paste the full JD text. **Never guess or reconstruct JD content from the company name, job title, or URL slug alone** — an incomplete real JD is fine to work with once flagged; a guessed one is not.
- If the user pastes JD text directly, use it as-is.

**CV:**
- A local file path ending in `.pdf`, `.md`, or `.txt` → read it directly with the `Read` tool. Claude Code reads PDF and Markdown natively — no conversion or parsing step needed.
- A `.docx` file → `Read` may not handle it reliably; ask the user to paste the text or export it to PDF first.
- Pasted CV text → use as-is.
- Treat the CV as one flat block of text. Do not try to force it into a rigid schema — extract what you need for each stage directly from the real content.
- If the CV is too thin to say anything meaningful (a one-line headline, no work history) → say so and ask for a fuller version before running Stage 2 onward. Stage 1 (JD decode) doesn't need the CV and can still run.

**Missing input:** if either the JD or the CV is missing, ask for the missing one — one question at a time, JD first. Don't bundle both requests into one message.

## Core Principles

These apply to every stage. Each stage prompt file references this section rather than restating it in full.

1. **Decode before anything else.** Stage 1 must complete before Stage 2 or 3 run. Never analyze match or tailor a CV against raw, unprocessed JD text.
2. **Never fabricate.** Every fact, number, employer, and achievement in any output must come from the user's real CV or something they explicitly told you. Tailoring means reorganizing, reframing, and re-quantifying real content — never inventing new experience.
3. **Verbatim JD requirement fidelity.** Any JD requirement referenced anywhere downstream — in the match analysis, in the tailored CV's alignment notes — must be an exact substring of the JD text. Not a paraphrase, not a cleaned-up version.
4. **`should_match` is evidence-gated, not a vibe.** Only classify a requirement as `should_match` when the CV shows strong, directly related adjacent evidence. When in doubt, classify it as a gap instead.
5. **One question at a time.** When you need more information from the user, ask for one thing, not a list.
6. **Disclose assumptions.** Every inference about company culture, seniority, or team stage must be labeled as inferred, with the JD language it's based on. Never present a guess as a fact.
7. **Standard disclaimer.** Every stage's output ends with: *"This content is generated by AI for reference only. Please review and adjust before use."* No other branding, footer, or attribution.

## Flow Control

- **Stage 1 → Stage 2 run back-to-back automatically** once both JD and CV are available. There's no meaningful pause point between them — Stage 2 structurally depends on Stage 1's output.
- **After Stage 2, gate on the recommendation status:**
  - `strong_candidate` → offer to generate the tailored CV and cover letter directly.
  - `needs_tailoring` → offer the tailored CV and cover letter, briefly explaining why tailoring matters here.
  - `not_recommended` → explain why, grounded in the Must-Have gaps and risk read. Do **not** auto-offer Stage 3. Ask whether the user wants to proceed anyway or see the full gap detail first.
- **Stage 3 only runs on user confirmation** — never auto-run it, even after a `strong_candidate` verdict.
- **After Stage 3, mention interview-prep-skill** is available for behavioral and technical interview prep — don't invoke it automatically, it's a separate skill.
- **Explicit single-stage requests skip all of the above.** If the user asks for just one stage ("just decode this JD"), run that stage alone without chaining into the rest.

## Output

Every job application persists to `~/cvpilot-applications/<company-slug>-<role-slug>-<YYYYMMDD>/application.html` — a fixed directory, not relative to wherever this skill happens to be invoked from. Each stage progressively updates the same file (Stage 1 creates it, Stage 2 appends to it regardless of verdict, Stage 3 appends to it only if it runs). Full naming logic, folder collision handling, and HTML structure live in [frameworks/application-report.md](frameworks/application-report.md) — read it before Stage 1's first write.

Chat responses are summaries with a pointer to the file (score, verdict, key points, file path) — not full-content dumps. The file is the source of truth; the user opens it for full detail.

## Reference Files

Load these on demand as each stage needs them — don't read the whole skill directory upfront.

**Prompts** (one per stage, read the matching file when that stage runs):
- [prompts/01-jd-decode.md](prompts/01-jd-decode.md)
- [prompts/02-match-analysis.md](prompts/02-match-analysis.md)
- [prompts/03-tailor-and-cover-letter.md](prompts/03-tailor-and-cover-letter.md)

**Frameworks** (reference material each stage prompt points to):
- [frameworks/decode-patterns.md](frameworks/decode-patterns.md) — recruiting-speak translation dictionary, used by Stage 1.
- [frameworks/match-classification.md](frameworks/match-classification.md) — classification rules and scoring formula, used by Stage 2.
- [frameworks/resume-tailoring.md](frameworks/resume-tailoring.md) — tailoring and cover-letter checklists, used by Stage 3.
- [frameworks/application-report.md](frameworks/application-report.md) — fixed output directory, folder naming, HTML structure, used by all three stages.
