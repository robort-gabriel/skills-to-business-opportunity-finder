---
name: niche-recommender
description: Score and rank candidate niches by demand, competition, and personal fit, then recommend the top profitable niches with a clear rationale traceable to the earlier research. Use this as stage 4 of the Skills-to-Business Opportunity Finder pipeline, after competitor-scanner has produced its competitor file, or standalone when the user asks "which of these ideas should I actually pursue" or "rank these business ideas".
---

# Niche Recommender

## Overview

Synthesizes `01-profile.md`, `02-market-demand.md`, and `03-competitors.md` for the same run into a ranked shortlist of the most promising niches, each with a plain rationale. This is the "which business should I actually build" decision point of the pipeline.

## Inputs

- `run_slug` (required): matches the run this continues.
- `run_date` (required): matches the run date.
- Reads all three prior output files for this run: `01-profile.md`, `02-market-demand.md`, `03-competitors.md`.

If any of the three input files is missing, stop and report which stage's output is missing rather than guessing its contents.

## Steps

1. Read all three input files in full.
2. Score every niche that made it through stage 3 on three factors, each rated low/medium/high with a one-line reason:
   - **Demand** (from `02-market-demand.md`'s signal strength)
   - **Competitive opening** (from `03-competitors.md`'s market read — "underserved" scores higher than "crowded")
   - **Personal fit** (from `01-profile.md` — skill-based niches score higher than pure interest-based ones, since they're faster to start credibly)
3. Rank niches by a simple heuristic: prioritize niches with at least medium on all three factors over niches that are high on one but low on another (e.g. huge demand but zero personal fit isn't a good first business). State the ranking logic briefly so the reasoning is auditable.
4. Select the **top 2-3 niches** to recommend. For each, write a short rationale paragraph citing the specific demand evidence and competitive opening that support it (pull direct references from stages 2-3, don't restate generically).
5. For niches that scored well on demand/competition but poorly on fit (or vice versa), note them as "worth revisiting" rather than dropping them silently, this is useful signal for the user even if not the top pick.
6. Write the result to `Content/Business-Opportunities/<run_slug>/<run_date>/04-recommended-niches.md`:
   ```markdown
   # Recommended Niches: <run_slug> (<run_date>)

   ## Scoring
   | Niche | Demand | Competitive opening | Personal fit |
   | --- | --- | --- | --- |
   | ... | ... | ... | ... |

   ## Top Picks
   1. **<Niche name>** — rationale: ... (cites demand + competitive evidence)
   2. ...

   ## Worth Revisiting
   - <Niche>: <why it didn't make the top picks, and under what condition it would>
   ```

## Output

`Content/Business-Opportunities/<run_slug>/<run_date>/04-recommended-niches.md` — hands off the top picks to `service-packager`.

## Error Handling

- Every score and ranking decision must trace back to a specific fact in the three input files. Never rank a niche higher based on an assumption not present in the research.
- If the research is thin for a niche, say the evidence is thin rather than padding the rationale.
