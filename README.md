# cvpilot-skill

A [Claude Code](https://claude.com/claude-code) skill toolkit for job hunting — turns a job posting and your CV into a decoded JD, an evidence-based match analysis, a tailored CV and cover letter, and CV-grounded behavioral/technical interview prep. English only, no fabricated content, no inflated scores.

It's a from-scratch and rebuild of the workflow in [CVpilot](https://github.com/zhiyuanMA/CVpilot) *(Chrome extension)*.

## What it does

`cvpilot-skill` is a thin router over two independent sub-skills that share a job posting and a CV as input:

### `application-skill` — stateless, one job at a time

1. **JD Decode** — a 5-layer breakdown of what the hiring manager actually wants versus recruiting-speak: Must-Haves, Nice-to-Haves, Hidden Signals (culture/pace/team-stage inferred from word choice), and level/team/stage inference.
2. **Match Analysis** — every JD requirement classified as `match` / `should_match` / `gaps` against your CV, using verbatim JD quoting and strict evidence rules (no credit for skills your CV doesn't actually show). Converts to a weighted, hard-capped numeric score and a `strong_candidate` / `needs_tailoring` / `not_recommended` verdict — never inflated.
3. **Tailored CV + Cover Letter** — an actual rewritten CV (not just suggestions), with every change shown as a diff back to the original, plus a 200–300 word cover letter. Never fabricates an achievement, a number, or a skill you don't have.

<img src="screenshots/JD%20decode.jpg" width="420" alt="JD Decode output — five layers translating a job posting into what the hiring manager actually wants"> <img src="screenshots/Match%20analysis.jpg" width="420" alt="Match Analysis output — match/should_match/gaps breakdown, weighted score, gap tiers, risk, and recommendation">

*JD Decode and Match Analysis from `application.html`.*

### `interview-prep-skill` — persistent, reused across every application

4. **Behavioral prep** — mines real STAR stories through a guided, one-question-at-a-time conversation, tags them by competency, and generates a JD-specific Top 20 questions with full STAR prep for the Top 5.
5. **Technical prep** — mines technical decision narratives (context → options considered → trade-offs → outcome → reflection) from your real projects, calibrated to the seniority level (Junior/Intermediate/Senior/Staff) the JD is actually hiring for.

<img src="screenshots/BQ%20top%2020%20question.jpg" width="420" alt="Behavioral prep Top 20 questions — grouped by category, each tied to a specific JD signal, with story coverage marked"> <img src="screenshots/Tech%20must%20practice.jpg" width="420" alt="Technical prep Must-Practice section — full Context/Decision/Options/Reasoning/Outcome/Reflection narratives">

<img src="screenshots/Tech%20question.jpg" width="420" alt="Technical prep question list by domain and honest gap list">

*Behavioral and technical prep from `behavioral-prep.html` / `technical-prep.html` — note the honest gap flags rather than generic filler questions.*

Both mining engines default to **comprehensive** mode on a thin story bank (mine broadly across your whole background) and **targeted** mode once the bank has solid coverage (mine just the gap) — a bank built one JD-gap at a time never ends up covering what you actually have to offer.

## Why two sub-skills

`application-skill` is stateless — decode, match, tailor, done, nothing persists between different jobs. `interview-prep-skill` is deliberately *not* stateless — its story bank is meant to accumulate across every job you ever prep for, so a story mined once doesn't need to be re-derived from scratch for the next application.

## Output

Everything about one job application lives in one folder:

```
~/cvpilot-applications/<company-slug>-<role-slug>-<YYYYMMDD>/
├── application.html        # JD decode + match analysis + tailored CV + cover letter
├── behavioral-prep.html    # Top 20 + Top 5 STAR, once interview-prep-skill runs
└── technical-prep.html     # level-calibrated technical questions + narratives
```

- Written **progressively** — the JD decode and match analysis persist even for jobs you decide not to pursue (`not_recommended`), since that record has its own value.
- `interview-prep-skill` reads the **tailored CV**, not your original one, once it exists — that's what the interviewer will actually have seen.
- A separate, cross-job **story bank** (`interview-prep-skill/story-bank/`) holds your mined behavioral stories and technical narratives — this is the part meant to grow over time and outlive any single application.

## Install

```bash
# clone this repo, then symlink it into Claude Code's skills directory
ln -s /path/to/cvpilot-skill ~/.claude/skills/cvpilot-skill
```

Claude Code discovers skills at `~/.claude/skills/<name>/SKILL.md` — one level deep. A symlink means edits to the repo take effect immediately in new sessions, no reinstall needed. (Restart or start a new Claude Code session for it to be picked up — it won't appear mid-conversation.)

To scope it to a single project instead of globally, symlink into that project's `.claude/skills/` directory instead.

## Usage

Just talk to Claude Code naturally — the skill's `description` frontmatter drives discovery, no slash command required:

> Paste a Seek/LinkedIn job link and your CV — "should I apply to this?", "tailor my resume for this role", "write me a cover letter"

> "Prep me for behavioral questions for this role" / "help me build my story bank" / "quiz me on technical questions for this"

## Design principles

- **Never fabricate.** Every claim, number, and story traces back to your real CV or your own account, confirmed with you.
- **Verbatim JD fidelity.** Every requirement referenced anywhere downstream is an exact quote from the JD, never a paraphrase.
- **Evidence over vibes.** `should_match` requires strong adjacent evidence and a genuine "it'd be surprising if they didn't have this" bar — when in doubt, it's a gap, not a maybe.
- **Conservative scoring.** Hard caps when Must-Haves are missing; scores are always a range, never a flattering single point.
- **Honest gaps.** Interview prep flags what isn't covered yet rather than papering over it with generic advice.

## Repo layout

```
cvpilot-skill/
├── SKILL.md                    # router
├── application-skill/
│   ├── SKILL.md
│   ├── prompts/                # one file per stage
│   └── frameworks/             # scoring rules, dictionaries, HTML/CSS spec
└── interview-prep-skill/
    ├── SKILL.md
    ├── prompts/
    ├── frameworks/
    └── story-bank/              # your mined stories persist here (gitignored except templates)
```
