# Application Report — Persistence, Folder Naming, HTML Structure

Reference framework for all three application-skill stages. Defines where and how each job application's output gets persisted, so it survives past the current conversation and so interview-prep-skill can read it back later.

---

## 1. Fixed Root Directory

All job applications persist under:

```
~/cvpilot-applications/
```

This is a fixed path, not relative to the current working directory — the whole point is that it's discoverable in any future session, from any working directory, by this skill or by interview-prep-skill. Create it if it doesn't exist yet.

---

## 2. Per-Job Folder Naming

Each job application gets one subfolder:

```
~/cvpilot-applications/<slug>/
```

- **When company and role are both clearly known** (the normal case — a Seek/LinkedIn posting, or pasted JD text with a named company): auto-generate `<company-slug>-<role-slug>-<YYYYMMDD>`, lowercase, hyphenated, special characters stripped. Example: `air-new-zealand-software-engineer-microservices-20260804`.
- **When the company isn't disclosed** (e.g., a recruiter/headhunter reaches out with a blind JD, no company named) — don't guess or invent a placeholder company name. Ask the user directly for a short label to use instead, e.g. "recruiter-fintech-backend-role". Use whatever they give you, slugified the same way.
- **Collision handling**: if a folder with that exact slug already exists (e.g., re-decoding the same JD same day), check whether it's genuinely the same job — if so, update the existing folder's `application.html` rather than creating a duplicate. If it's a different job that happens to collide (rare), append `-2`, `-3`, etc.

---

## 3. What Gets Persisted, and When

One file per job: `~/cvpilot-applications/<slug>/application.html`. It's written **progressively** — each stage appends or updates its own section rather than the file only appearing at the end:

- **After Stage 1 (JD Decode)**: create the folder (if new) and write `application.html` with the header + JD Decode section. Status: `decoded`.
- **After Stage 2 (Match Analysis)**: update the same file, appending the Match Analysis section — **regardless of the recommendation verdict**, including `not_recommended`. A record of "why I decided not to apply" has its own value, and it avoids re-decoding the same JD if it resurfaces later. Status: `matched`.
- **After Stage 3 (Tailor + Cover Letter)**: update the same file, appending the Tailored CV and Cover Letter sections — only if Stage 3 actually runs (it's gated on user confirmation, and skipped entirely for `not_recommended`). Status: `tailored`.

Use the `Edit` or `Write` tool to update `application.html` in place — don't create separate files per stage. Re-read the current file before editing it if there's any chance it already has content from an earlier stage in this or a prior session.

---

## 4. HTML Structure and Shared Design System

Single-file HTML, clean and readable — not the elaborate branded "editorial" design system some reference templates use, but more polished than a bare unstyled document. No author branding, no social links, no bilingual toggle (English only, per this skill's Core Principles).

**This exact CSS block is duplicated verbatim in `interview-prep-skill/frameworks/prep-report.md`** (its own "Shared CSS block" section), not just referenced — every generated HTML file must be self-contained (no external stylesheet), so each skill's framework file needs the literal, ready-to-use CSS rather than a pointer to the other one. **If this block changes, update both files together.**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>{{Company}} — {{Role}}</title>
<style>
  :root {
    --bg: #fafafa; --surface: #ffffff; --border: #e5e7eb;
    --text: #1f2328; --text-muted: #6b7280;
    --accent: #4f46e5; --accent-soft: #eef2ff;
    --green: #059669; --green-soft: #ecfdf5;
    --amber: #b45309; --amber-soft: #fffbeb;
    --red: #b91c1c; --red-soft: #fef2f2;
    --blue: #1d4ed8; --blue-soft: #eff6ff;
    --radius: 10px;
  }
  * { box-sizing: border-box; }
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
    background: var(--bg); color: var(--text);
    max-width: 880px; margin: 0 auto; padding: 3rem 1.5rem 5rem; line-height: 1.6;
  }
  header { margin-bottom: 2.5rem; }
  h1 { font-size: 1.8rem; font-weight: 700; margin: 0 0 0.5rem; letter-spacing: -0.01em; }
  h2 { font-size: 1.25rem; font-weight: 600; margin: 0 0 1rem; padding-bottom: 0.5rem; border-bottom: 2px solid var(--border); }
  h3 { font-size: 1.05rem; font-weight: 600; margin: 1.5rem 0 0.75rem; color: var(--accent); }
  .meta { color: var(--text-muted); font-size: 0.9rem; display: flex; gap: 0.5rem; align-items: center; flex-wrap: wrap; }
  .badge { display: inline-block; padding: 0.2rem 0.7rem; border-radius: 999px; font-size: 0.8rem; font-weight: 600; }
  .badge.decoded { background: var(--blue-soft); color: var(--blue); }
  .badge.matched { background: var(--amber-soft); color: var(--amber); }
  .badge.tailored { background: var(--green-soft); color: var(--green); }
  .badge.not_recommended { background: var(--red-soft); color: var(--red); }
  .badge.ready { background: var(--green-soft); color: var(--green); }
  .badge.gap { background: var(--red-soft); color: var(--red); }
  .badge.priority { background: var(--amber-soft); color: var(--amber); }
  section.card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 1.75rem 2rem; margin-bottom: 2rem; box-shadow: 0 1px 2px rgba(0,0,0,0.03); }
  .score-highlight { font-size: 2rem; font-weight: 700; color: var(--accent); }
  table { border-collapse: collapse; width: 100%; margin: 1rem 0; font-size: 0.92rem; }
  th, td { border: 1px solid var(--border); padding: 0.6rem 0.75rem; text-align: left; vertical-align: top; }
  th { background: #f9fafb; font-weight: 600; }
  tr:nth-child(even) td { background: #fcfcfd; }
  blockquote { border-left: 3px solid var(--accent); margin: 0.75rem 0; padding: 0.5rem 1rem; background: var(--accent-soft); border-radius: 0 6px 6px 0; color: var(--text); }
  pre { white-space: pre-wrap; background: #f9fafb; border: 1px solid var(--border); border-radius: 6px; padding: 1rem; font-size: 0.88rem; }
  code { background: #f1f1f3; padding: 0.15rem 0.4rem; border-radius: 4px; font-size: 0.9em; }
  .disclaimer { color: var(--text-muted); font-size: 0.85rem; border-top: 1px solid var(--border); padding-top: 1.25rem; margin-top: 3rem; }
  .diff-orig { color: var(--red); text-decoration: line-through; }
  .diff-new { color: var(--green); }
  @media print { body { max-width: 100%; background: white; } section.card { box-shadow: none; border: 1px solid #ccc; } }
</style>
</head>
<body>

<header>
  <h1>{{Company}} — {{Role}}</h1>
  <p class="meta">
    Location: {{location}} · Decoded: {{decoded_date}} ·
    <span class="badge {{status}}">{{status}}</span>
  </p>
</header>

<section id="jd-decode" class="card">
  <h2>JD Decode</h2>
  {{Stage 1 output — five layers}}
</section>

<section id="match-analysis" class="card">
  <h2>Match Analysis</h2>
  {{Stage 2 output — match/should_match/gaps, score (use <span class="score-highlight">72–80%</span> for the headline number), gap tiers, risk, recommendation}}
</section>

<section id="tailored-cv" class="card">
  <h2>Tailored CV</h2>
  {{Stage 3 output — tailored CV + diff list (use .diff-orig / .diff-new spans), only present if Stage 3 ran}}
</section>

<section id="cover-letter" class="card">
  <h2>Cover Letter</h2>
  {{Stage 3 output — cover letter text, only present if Stage 3 ran}}
</section>

<p class="disclaimer">This content is generated by AI for reference only. Please review and adjust before use. Last updated: {{last_updated_date}}.</p>

</body>
</html>
```

Sections that haven't run yet simply don't exist in the file yet — don't pre-populate empty placeholder sections. Update the `badge` class/text and `last_updated_date` on every write. Use `<blockquote>` for verbatim JD quotes, `<table>` for the match/should_match/gaps breakdown and gap-tier lists where a tabular view reads more easily than a bullet list, and `.score-highlight` for the headline match-score number.

---

## 5. Chat Behavior Change

Because output now persists to a file, chat responses go back to being **summaries with a pointer to the file**, not full-content dumps — give the user the headline result (score, verdict, key points) plus the file path, and let them open the file for full detail. This reverses the earlier "no files, must show everything in chat" rule from when this skill was console-only.
