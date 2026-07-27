---
name: skill-profile-analyzer
description: Turn a person's raw skills, experience, and interests into a structured profile and a shortlist of candidate AI-service or business niches. Use this as stage 1 of the Skills-to-Business Opportunity Finder pipeline, before market-demand-researcher runs, or standalone when the user asks "what business could I start with my skills" or "turn my background into service ideas".
---

# Skill Profile Analyzer

## Overview

Reads a free-text description of someone's skills, professional experience, and interests, and converts it into a structured profile plus 5-8 candidate niches worth investigating further. Every candidate niche must be traceable to a specific skill, experience, or interest the person actually listed, no invented backgrounds.

## Inputs

- `raw_profile` (required): free text describing skills, work history, tools used, interests, and any constraints (time available, budget, preferred working style e.g. solo/agency/freelance).
- `run_slug` (optional): short kebab-case identifier for this run, derived from the person's name or main skill area if not given (e.g. `robort-ai-automation`).
- `run_date` (optional, default today, `YYYY-MM-DD`).

If `raw_profile` is missing or too thin to extract at least 2-3 real skills, stop and ask for more detail rather than inventing a background.

## Steps

1. Extract a structured profile from `raw_profile`:
   - **Hard skills** (technical/professional abilities, tools, certifications)
   - **Domain experience** (industries worked in, roles held, years of experience where stated)
   - **Interests** (topics the person is drawn to, even without direct experience)
   - **Constraints** (time, budget, solo vs. team, stated preferences or exclusions)
2. Cross-reference hard skills + domain experience + interests to generate 5-8 **candidate niches**: specific, narrow service or product ideas (not broad categories like "consulting"). Each candidate niche must cite which listed skill(s)/experience/interest(s) it draws from.
3. For each candidate niche, note a one-line **why-this-fits** rationale and flag whether it leans more on existing hard skills (lower learning curve) or on interests (higher learning curve, needs validation).
4. Do not rank or score niches here, that's `niche-recommender`'s job downstream. This stage only generates and grounds the candidate list.
5. Write the result to `Content/Business-Opportunities/<run_slug>/<run_date>/01-profile.md` using this structure:
   ```markdown
   # Profile: <run_slug> (<run_date>)

   ## Structured Profile
   - Hard skills: ...
   - Domain experience: ...
   - Interests: ...
   - Constraints: ...

   ## Candidate Niches
   1. **<Niche name>** — draws from: <skill/experience/interest cited>. Why it fits: <one line>. Basis: skill-based | interest-based.
   2. ...
   ```

## Output

`Content/Business-Opportunities/<run_slug>/<run_date>/01-profile.md` — hands off `run_slug`, `run_date`, and the candidate niche list to `market-demand-researcher`.

## Error Handling

- If `raw_profile` yields fewer than 2 real skills/experiences, stop and ask the user for more input rather than padding the list with generic niches.
- Never invent a skill, credential, or years of experience the person didn't state.
