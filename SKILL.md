---
name: cvpilot-skill
description: "Job-search copilot toolkit, routing to two independent sub-skills that share a Seek NZ/AU (or LinkedIn) job posting and a candidate's CV as input. (1) application-skill: JD decode, evidence-based match analysis (match/should_match/gaps with verbatim JD quoting and a hard-capped numeric score), tailored CV rewrite, and a 200-300 word cover letter — presented directly in chat, no files. (2) interview-prep-skill: behavioral and technical interview preparation, backed by a persistent, reusable story bank of STAR stories and technical decision narratives so a candidate mines their real experience once and reuses it across every future application; technical prep is calibrated to the target seniority level (Junior/Intermediate/Senior/Staff) inferred from the JD. Never fabricates a claim, a story, or a number — everything traces back to the candidate's real CV or their own account. Trigger phrases: job description, JD, Seek job, Seek NZ, Seek AU, LinkedIn job posting, should I apply, match score, resume match, CV match, gap analysis, tailor my resume, tailor my CV, cover letter, behavioral interview, BQ prep, STAR method, tell me about a time, technical interview, system design interview, mock interview, story bank, interview prep, job search, career coach, application strategy."
---

# cvpilot-skill

A job-search toolkit split into two independent sub-skills. Route to the one that matches what the user is asking for — both take the same two inputs (a job posting and a CV) but serve different moments in the application process.

## Routing

| User says / gives you | Route to |
|---|---|
| A Seek/LinkedIn job link + CV, "should I apply," "match my resume," "tailor my CV," "write me a cover letter" | [application-skill](application-skill/SKILL.md) |
| "Prep me for behavioral questions," "tell me about a time...," "mock interview," "build my story bank," "technical interview prep," "system design questions for this role" | [interview-prep-skill](interview-prep-skill/SKILL.md) |
| Ambiguous — e.g. just "help me with this job" | Ask: "Do you want help with the application itself (JD match, tailored CV, cover letter), or interview prep (behavioral/technical questions)?" |

If a user has just finished application-skill's pipeline in this conversation, offer interview-prep-skill as the natural next step — it will reuse the JD and CV context already gathered rather than asking again.

## Why two sub-skills, not one

The two serve genuinely different lifecycles. application-skill is stateless — decode, match, tailor, done, nothing persists. interview-prep-skill is explicitly *not* stateless — its story bank is meant to accumulate across every application a candidate ever preps for, so behavioral and technical stories mined once don't need to be re-derived from scratch for the next job. Splitting them keeps that distinction structurally clear rather than bolting persistence onto only part of one skill.

## Install

Each sub-skill is self-contained. Point Claude Code at this folder (or symlink it into `~/.claude/skills/`) and both `application-skill/SKILL.md` and `interview-prep-skill/SKILL.md` become independently discoverable — Claude will route to the right one based on what you ask for, same as this file's routing table.
