# Prep Report — HTML Structure for behavioral-prep.html / technical-prep.html

Reference framework for Stage 2 (`prompts/02-behavioral-prep.md`) and Stage 4 (`prompts/04-technical-prep.md`). Both write into the same job folder application-skill uses (`~/cvpilot-applications/<slug>/`), so both use the **exact same CSS** as application-skill's `application.html` — the block below is duplicated verbatim from `../../application-skill/frameworks/application-report.md` §4, not just referenced, since every generated HTML file must be self-contained (no external stylesheet, so it still renders correctly offline, printed, or emailed as a single file). **If the color scheme or layout changes, update both files together** — this one and `application-report.md` §4.

No author branding, no bilingual toggle (English only), per this skill's Core Principles.

### Shared CSS block (embed this verbatim inside every `<style>` tag below)

```css
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
```

---

## behavioral-prep.html structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Behavioral Prep — {{Company}} — {{Role}}</title>
<style>
  {{paste the "Shared CSS block" from the top of this file, verbatim}}
</style>
</head>
<body>

<header>
  <h1>Behavioral Interview Prep</h1>
  <p class="meta">{{Company}} — {{Role}} · Generated: {{date}}</p>
</header>

<section class="card">
  <h2>Bank Status</h2>
  <p>{{one or two sentences: bank maturity at generation time, e.g. "thin — 1 story banked, covering 3 of ~7 relevant competencies"}}</p>
</section>

<section class="card">
  <h2>Must-Practice</h2>
  <!-- one block per must-practice question, in order -->
  <h3><span class="badge ready">READY</span> {{question text}}</h3>
  <p><strong>S</strong> {{...}}</p>
  <p><strong>T</strong> {{...}}</p>
  <p><strong>A</strong> {{...}}</p>
  <p><strong>R</strong> {{...}}</p>
  <p><em>Source: story-bank/{{slug}}.md</em></p>

  <h3><span class="badge priority">NOT YET MINED — priority</span> {{question text}}</h3>
  <p>{{why this is a priority gap, and what raw CV material exists, if any}}</p>
</section>

<section class="card">
  <h2>Top 20 Questions</h2>
  <table>
    <tr><th>Category</th><th>Question</th><th>Tests</th><th>Why this role asks it</th><th>Story</th></tr>
    <!-- one row per question, grouped by category (General / Company-Values / Role-Craft / Level-Stage) -->
    <tr><td>General</td><td>{{question}}</td><td>{{competency}}</td><td>{{JD tie}}</td><td><span class="badge ready">✓</span> or <span class="badge gap">Gap</span></td></tr>
  </table>
</section>

<section class="card">
  <h2>Gap List — Priority to Mine</h2>
  <ol>
    <li>{{gap, ranked by priority, with reasoning}}</li>
  </ol>
</section>

<p class="disclaimer">This content is generated by AI for reference only. Please review and adjust before use.</p>

</body>
</html>
```

---

## technical-prep.html structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Technical Prep — {{Company}} — {{Role}}</title>
<style>
  {{paste the "Shared CSS block" from the top of this file, verbatim}}
</style>
</head>
<body>

<header>
  <h1>Technical Interview Prep</h1>
  <p class="meta">{{Company}} — {{Role}} · Target level: <span class="score-highlight" style="font-size:1.1rem;">{{level}}</span> · Generated: {{date}}</p>
</header>

<section class="card">
  <h2>Target Level and Bank Status</h2>
  <p>{{level reasoning — why this level was chosen}}</p>
  <p>{{bank maturity at generation time}}</p>
</section>

<section class="card">
  <h2>Must-Practice</h2>
  <!-- one block per must-practice question -->
  <h3><span class="badge ready">READY</span> {{question text}}</h3>
  <p><strong>Context</strong> {{...}}</p>
  <p><strong>Decision point</strong> {{...}}</p>
  <p><strong>Options considered</strong> {{...}}</p>
  <p><strong>Decision &amp; reasoning</strong> {{...}}</p>
  <p><strong>Outcome</strong> {{...}}</p>
  <p><strong>Reflection</strong> {{...}}</p>
  <p><em>Source: story-bank/{{slug}}.md</em></p>

  <h3><span class="badge priority">NOT YET MINED — priority</span> {{question text}}</h3>
  <p>{{why this is a priority gap, and what raw CV material exists, if any}}</p>
</section>

<section class="card">
  <h2>Question List by Domain</h2>
  <table>
    <tr><th>Domain</th><th>Question</th><th>Tests</th><th>Why this role asks it</th><th>Narrative</th></tr>
    <tr><td>{{domain}}</td><td>{{question}}</td><td>{{judgment being tested}}</td><td>{{JD tie}}</td><td><span class="badge ready">✓</span> or <span class="badge gap">Gap</span></td></tr>
  </table>
</section>

<section class="card">
  <h2>Gap List — Priority to Mine</h2>
  <ol>
    <li>{{gap, ranked by priority — include level mismatches here too, not just missing domains}}</li>
  </ol>
</section>

<p class="disclaimer">This content is generated by AI for reference only. Please review and adjust before use.</p>

</body>
</html>
```

---

## Notes

- `READY` questions pull their full narrative directly from the relevant `story-bank/*.md` entry — never re-derive or paraphrase it, copy the interview-ready version.
- `NOT YET MINED` questions never get a fabricated placeholder narrative — just the reasoning for why it's a gap and (if applicable) what raw CV material exists to mine from later.
- Reuse the `.badge` classes from the shared CSS (`ready` = green, `priority`/`gap` = amber/red) so status reads consistently with `application.html`'s own status badge in the same folder.
