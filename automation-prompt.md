# Skills-to-Business Opportunity Finder — Automation Prompt

## Objective

Turn `{{RAW_PROFILE}}`'s skills, experience, and interests into a ranked, market-validated business opportunity with concrete service packages and pricing, by running the five project-local skills in sequence: `skill-profile-analyzer` -> `market-demand-researcher` -> `competitor-scanner` -> `niche-recommender` -> `service-packager`.

## Inputs

- `raw_profile` (required): `{{RAW_PROFILE}}` — free text describing skills, work history, tools used, interests, and any constraints (time available, budget, solo vs. agency preference).
- `run_slug` (optional): `{{RUN_SLUG}}` — short kebab-case identifier for this run; derived from the person's name or main skill area if not given.

## Steps

1. Run `skill-profile-analyzer` (`Skills/skill-profile-analyzer/SKILL.md`) on `raw_profile`. Output: `Content/Business-Opportunities/<run_slug>/<run_date>/01-profile.md`.
2. Run `market-demand-researcher` (`Skills/market-demand-researcher/SKILL.md`) on the candidate niches from step 1, using only `web_search`, `web_research`, and `x_search`. Output: `02-market-demand.md` in the same folder.
3. Run `competitor-scanner` (`Skills/competitor-scanner/SKILL.md`) on the niches from step 2. Output: `03-competitors.md` in the same folder.
4. Run `niche-recommender` (`Skills/niche-recommender/SKILL.md`) on all three prior files, producing a ranked top 2-3. Output: `04-recommended-niches.md` in the same folder.
5. Run `service-packager` (`Skills/service-packager/SKILL.md`) on the top pick(s), producing service tiers, pricing, and a positioning document. Output: `05-service-packages-pricing.md` in the same folder.
6. Do not fabricate a skill, demand signal, competitor, or price at any stage — only report what the person actually stated or what research actually found. Label estimated prices as estimates.

## Outputs

Saved under `Content/Business-Opportunities/<run_slug>/<run_date>/`:

- `01-profile.md`
- `02-market-demand.md`
- `03-competitors.md`
- `04-recommended-niches.md`
- `05-service-packages-pricing.md` (final deliverable: business ideas, service list, pricing, positioning document)

Plus a short chat/report summary: the top recommended niche, its demand/competition rationale, the package tiers and price range, and the output folder path.

## Error handling

- If `raw_profile` is missing or too thin to extract at least 2-3 real skills/experiences, stop and ask for more detail rather than inventing a background.
- If any stage's required input file is missing (e.g. `niche-recommender` can't find `03-competitors.md`), stop and report which stage failed rather than guessing its contents.
- If a niche turns up no real demand or competitor evidence, mark it accordingly rather than inventing supporting evidence — this is a valid, useful finding, not a failure.
