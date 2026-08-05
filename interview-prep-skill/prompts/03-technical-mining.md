# Stage 3 · Technical Story Mining

> See [SKILL.md](../SKILL.md) § Core Principles before executing this stage. Frameworks: [../frameworks/technical-narrative-framework.md](../frameworks/technical-narrative-framework.md), [../frameworks/technical-depth-by-level.md](../frameworks/technical-depth-by-level.md).

**Goal:** probe a candidate's real projects for the technical judgment and trade-off reasoning that a CV bullet point never shows, and save it as a reusable technical narrative. This is a conversation, not a questionnaire — one question at a time, and it takes real back-and-forth to get past a CV's flat description into an actual decision narrative.

**Bank first, always.** Check [../story-bank/_index.md](../story-bank/_index.md) for an existing technical narrative covering the domain/level you need before mining a new one.

**Two ways this stage gets triggered — both are normal:**

- **Comprehensive** — the user asks directly ("help me prep technical stories," "build out my technical narratives") or the bank is thin (see [04-technical-prep.md](04-technical-prep.md)'s bank maturity check). Mine across all of the candidate's apparent technical domains from their CV, not just the ones this specific JD happens to test — a bank built one JD-domain at a time never ends up covering the candidate's actual breadth. Default to this mode whenever the bank is thin, even if the immediate trigger was a specific JD.
- **Targeted** — [04-technical-prep.md](04-technical-prep.md) sends you here for one specific missing domain/level because the bank is otherwise already solid. In that case, mine just that domain rather than doing a full sweep.

If unsure which applies, ask: "Want to cover your main technical areas broadly, or just fill the one or two gaps for this application?"

---

## Layer 1 · Identify Domains and Target Level

1. From the CV, list the candidate's apparent technical domains (e.g. backend/distributed systems, frontend performance, data pipelines, ML infra, mobile, security, infrastructure/DevOps).
2. In **comprehensive mode**, plan to mine across most or all of these domains over the session. In **targeted mode**, cross-reference against the JD's technical Must-Haves and confirm with the user which specific domain(s) to mine.
3. Determine the target level per [../frameworks/technical-depth-by-level.md](../frameworks/technical-depth-by-level.md) — pull from the JD decode if one is available, or ask the user directly. In comprehensive mode without a specific JD in hand, ask the user what level(s) they're generally targeting. **This determines how deep to probe** — don't push a Junior-level project toward a fabricated system-design narrative it doesn't have, and don't let a Staff-level candidate settle for an implementation-level answer that undersells their actual scope.

---

## Layer 2 · Deep-Dig

For each domain, pick 1-2 real CV projects and probe past the CV's flat bullet into an actual decision narrative, following [../frameworks/technical-narrative-framework.md](../frameworks/technical-narrative-framework.md)'s structure (full form for design-level decisions, short form for implementation/debugging stories — use the target level to judge which fits).

Question progression, one at a time:

1. **Context** — "What was the system/project, and what were the real constraints? (scale, deadline, team size, legacy constraints)"
2. **Decision point** — "What specifically needed to be solved or decided here?"
3. **Options** — "What approaches did you actually consider? What were the trade-offs of each?" If the candidate can only name one approach, don't invent a second — see Common Snags.
4. **Decision & reasoning** — "Why did you choose the one you did? What made you confident, or what were you unsure about?"
5. **Outcome** — "What happened? Do you have numbers — latency, error rate, cost, adoption, whatever's relevant?"
6. **Reflection** — "Looking back, would you make the same call? What would you do differently now?"

Whenever the answer stays at "we decided" or "the team chose," redirect: **"What was your specific judgment call in that decision?"** — same discipline as behavioral mining, applied to technical ownership instead of task ownership.

---

## Layer 3 · Tag by Domain and Level

1. Tag `tech_domain` (e.g. `distributed-systems`, `frontend-performance`) — one or two, not a long list.
2. Tag `level_fit` using [../frameworks/technical-depth-by-level.md](../frameworks/technical-depth-by-level.md) — which target level(s) does this narrative's scope and reasoning actually support? Be honest here: a narrative that's really Intermediate-scoped shouldn't be tagged Senior just because the candidate is targeting Senior roles.

---

## Layer 4 · Save to Bank

1. Write the narrative to `../story-bank/<slug>.md` using [../story-bank/_technical-template.md](../story-bank/_technical-template.md).
2. Update [../story-bank/_index.md](../story-bank/_index.md) — add it to the technical-domain table and the "all entries" table.
3. Confirm with the user and offer to mine another domain, or move on to generating prep.

---

## Stuck? Troubleshooting

| Symptom | Handling |
|---|---|
| Candidate can only name one option, not real alternatives | Don't invent a second option to force the full-form structure. Use the short form instead, or have them honestly say "there wasn't really a choice here, but here's why I was confident" — that's a legitimate answer. |
| CV project doesn't match the target level (e.g. Senior candidate, only Junior-scoped projects available) | Say so directly rather than inflating the narrative. Ask whether they have a more senior-scoped project not reflected on the CV, or flag this as a genuine gap for Stage 4 to surface. |
| No hard numbers available | Fall back to qualitative scope (system size, team impact, what broke without the fix) and mark `metrics: not yet confirmed` — don't estimate on the candidate's behalf. |
| Candidate undersells a genuinely senior decision as "just what I was told to do" | Probe once more — "was there a point where you had to decide the approach yourself, even within those instructions?" — before accepting it's not there. |
