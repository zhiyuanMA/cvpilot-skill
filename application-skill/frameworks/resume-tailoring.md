# Resume Tailoring — Rules, Checklist, and Diff Format

Reference framework for Stage 3 (`prompts/03-tailor-and-cover-letter.md`).

---

## 1. Shared Principles

- **Never fabricate.** Every rewrite draws only on facts already present in the candidate's real CV. Reorganize, highlight, re-quantify, and translate into the JD's vocabulary — never invent a new achievement, number, or responsibility.
- **Never inflate a verb.** "Contributed to X" does not become "led X." If the CV says "participated," the tailored version says something equivalent to "participated," phrased more sharply — not something implying ownership the candidate didn't have.
- **Numbers, scope, and titles are always confirmed with the user**, never guessed. If the CV lacks a number for a claim that would benefit from one, ask the user for it or a conservative estimate — don't write one in.
- **This tailors for one JD.** It's not a general resume quality overhaul. If the candidate wants broader resume polishing beyond this specific application, say so explicitly rather than trying to do both at once.

---

## 2. Tailored CV Requirements (merged ATS + hiring-manager readable)

Produce one CV, not separate ATS/Recruiter/HM variants — the requirements below are compatible with both an applicant tracking system and a human reader:

- **Standard section headers** (Experience, Education, Skills, etc.) — no creative renaming that a parser might miss.
- **No tables, multi-column layouts, or embedded images/icons** — plain text structure that both ATS parsers and humans read cleanly.
- **JD keyword coverage**: JD-native terms (verbs and nouns from the Must-Haves) should appear 2–4 times across the Skills section and relevant bullets — naturally, not stuffed to the point of reading like keyword-spam.
- **Bullet structure**: prefer "problem/context → judgment made → action taken → result" over a flat list of actions. This surfaces the candidate's thinking, not just their task list.
- **Hidden-Signal-aligned language**: if Stage 1 flagged strong Hidden Signals (e.g. ownership, ambiguity, cross-functional influence), make sure at least one bullet per relevant role reflects that language honestly, if the underlying fact supports it.
- **Preserve 1–2 "hook" details** per key role — specific enough that an interviewer would naturally follow up on them. Don't sand every detail down into generic corporate phrasing.
- **Numbers and impact stay prominent** — don't bury a quantified result at the end of a long sentence.
- **Section order**: Name & Contact → Headline/Summary → Experience → Education → Skills → Selected Projects (only if relevant and present in the source CV).
- **Least relevant / oldest experience** can be compressed to a line or two — don't force equal space onto everything.

---

## 3. Diff Output Format

For every bullet you add, cut, or meaningfully change, show the change explicitly — don't just hand over a final document and expect the user to spot what moved. This is the core value of the tailoring step; don't skip it.

```
[Change #1 — Experience: Company Name]

Original:
> Led design for the internal analytics dashboard

Tailored:
> Led end-to-end design of the analytics dashboard used by 200+ internal
> sales reps, partnering with PM and engineering to cut report-building
> time from 15 minutes to under 2.

Aligns to:
- Must-Have: "end-to-end product design experience" — "end-to-end design"
- Hidden Signal: cross-functional ownership — "partnering with PM and engineering"

Based on CV fact: original CV said "Led design for the internal analytics
dashboard used by sales team"; user confirmed the 200+ user count and the
15-min → 2-min improvement in conversation.
```

Give one diff block per meaningful change — not just a single before/after for the whole document.

---

## 4. Cover Letter Checklist

- 200–300 words total.
- Concise and role-specific — this is not a generic template with the company name swapped in.
- Aligns the candidate's real experience directly to the JD's requirements; ideally references 1–2 specific things from the match analysis (a strong `match` item, and if relevant, how a `should_match` item connects).
- Professional tone, first person, no invented achievements.
- Ends with genuine interest in the specific role/company — avoid boilerplate closing lines.

---

## 5. Common Snags

| Symptom | Handling |
|---|---|
| CV is missing a number for a claim | Don't invent one. Ask: "This would land harder with a number — do you have one, or a conservative estimate?" |
| User wants to "exaggerate a bit" | Push back directly: exaggeration that can't be backed up in an interview backfires — every line on a tailored CV gets followed up on. |
| CV and JD are too far apart to tailor meaningfully | Don't force it. Point back to the Stage 2 verdict — if it was `not_recommended`, tailoring isn't the right next step. |
| User only wants one deliverable (CV or cover letter, not both) | Produce just the one they asked for, but mention the other is available if they want it. |
