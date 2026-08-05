# Technical Depth by Level

Reference framework for Stage 4 (`prompts/04-technical-prep.md`) and Stage 3 (`prompts/03-technical-mining.md`). Defines what "good" looks like at each seniority level, so both the mined narratives and the generated questions are calibrated to the level the JD is actually hiring for — a Junior-level prep session shouldn't expect Staff-level system-design narratives, and a Staff-level prep session shouldn't stop at "how would you implement X."

---

## Determining the target level

Pull this from the condensed JD decode (see interview-prep-skill's Input Intake): title, explicit years-of-experience language, and Level/Title signals from `../application-skill/frameworks/decode-patterns.md` §2 ("Level / Title signals"). If the JD is genuinely ambiguous about level, **ask the user directly** which level they're interviewing for rather than guessing — this materially changes what "good" looks like below, so don't proceed on an assumption.

---

## Junior / Entry

**What's actually being evaluated:** correctness, following established patterns, debugging with some guidance, fundamentals.

**Narrative scope:** a single feature or well-scoped task within an existing system. The interesting content is *how they approached learning/solving it*, not an architecture decision — they usually won't have made one yet, and that's fine.

**Question shapes:** "How would you implement X?" / "Walk me through how you'd debug Y." / "What does this piece of code do, and how would you improve it?" / "Tell me about a bug you found and how you tracked it down."

**Common miscalibration to avoid:** don't force a Junior candidate's story into an "options considered, trade-offs weighed" shape if that's not really what happened — a clear, honest account of learning and problem-solving is the right bar here, not manufactured strategic depth.

---

## Intermediate / Mid

**What's actually being evaluated:** independent ownership of a bounded component, understanding trade-offs within that scope, debugging production issues without hand-holding.

**Narrative scope:** one component or service they owned end-to-end. Should include at least one real judgment call — a design choice within their scope, not necessarily one that affected other teams.

**Question shapes:** "Tell me about a technical decision you made on a project you owned." / "A time you had to debug something in production." / "How did you decide between two approaches to X?"

**Common miscalibration to avoid:** don't undersell it into a Junior-shaped "I followed the existing pattern" story if there was a real decision — but also don't inflate a component-level choice into a system-wide one it wasn't.

---

## Senior

**What's actually being evaluated:** system-level design decisions, trade-offs that span components or teams, driving technical direction for a project, mentoring.

**Narrative scope:** a system design decision with real trade-offs (performance vs. simplicity, build vs. buy, consistency vs. availability, etc.) and evidence of influencing others' technical thinking, not just executing their own.

**Question shapes:** "Walk me through a system you designed and why you made the choices you did." / "Tell me about a time you had to make a call with significant trade-offs and limited time to decide." / "How did you bring other engineers along on a technical direction?"

**Common miscalibration to avoid:** a Senior narrative that never says "and here's why I rejected the alternative" is under-scoped — the trade-off reasoning is the point, not just the final architecture.

---

## Staff / Principal

**What's actually being evaluated:** technical strategy across multiple teams or the org, resolving ambiguity that doesn't have an obvious owner, technical risk management, setting direction that other senior engineers follow.

**Narrative scope:** a decision or initiative whose blast radius extends beyond their own team — cross-team technical alignment, a technical bet made under real uncertainty, or a case where they had to influence direction without formal authority over the people involved.

**Question shapes:** "Tell me about a time you influenced technical direction beyond your own team." / "A time you had to make a call with major technical risk and incomplete information." / "How do you decide when to invest in paying down technical debt versus shipping features, at an org level?"

**Common miscalibration to avoid:** a Staff-level narrative framed entirely as "I personally built X" without any cross-team influence or ambiguity-navigation angle is really a Senior story — don't let a strong IC story stand in for Staff-level scope without genuinely checking it has that broader dimension.
