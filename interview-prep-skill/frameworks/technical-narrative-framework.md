# Technical Narrative Framework

Reference framework for Stage 3 (`prompts/03-technical-mining.md`) and Stage 4 (`prompts/04-technical-prep.md`). Behavioral questions fit STAR well; technical deep-dives usually don't — "Situation/Task" undersells the actual content, which is the *reasoning behind a technical decision*. Use this structure instead.

## Full form (system design / architecture-level decisions)

```
Context      — the system/project, its scale, and the real constraints in play
             (traffic, team size, deadline, legacy constraints, etc.)
Decision point — what specifically needed to be solved or decided; why it mattered
Options considered — at least two real options, each with genuine trade-offs
             (not a strawman option that exists only to be rejected)
Decision & reasoning — what was chosen, and the actual judgment behind it —
             this is the core of the narrative, budget the most time here
Outcome      — what happened, with numbers where possible
Reflection   — what they'd do differently now, or what they learned
```

Use the full form for: system design questions, architecture decisions, build-vs-buy calls, anything where "why this and not that" is the point.

## Short form (implementation / debugging stories)

```
Context   — what was being built or what broke
Problem   — the specific technical issue
Approach  — what they did to solve or investigate it
Outcome   — the result, and (if relevant) what they'd watch for next time
```

Use the short form for: debugging stories, "how would you implement X," and other narratives where there isn't a genuine multi-option trade-off to walk through — forcing the full form onto these produces a padded, unconvincing "options considered" section that isn't really there.

## Delivery discipline

- **Budget the most time on "Decision & reasoning" / "Approach"** — same principle as STAR's Action-heavy time budget (see `../../application-skill` for the behavioral equivalent). A technical narrative that's mostly Context and Outcome, with the actual reasoning compressed to one sentence, is under-cooked.
- **Never fabricate options that weren't actually considered.** If, honestly, there was only one real option, say so — the interviewer would rather hear an honest "there wasn't really a choice here, but here's why I was confident in it" than an invented debate.
- **Numbers get confirmed with the user, never estimated on their behalf.** Same discipline as everywhere else in this skill.
