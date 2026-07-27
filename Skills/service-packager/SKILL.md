---
name: service-packager
description: Turn a recommended niche into concrete service packages, tiered pricing, and a one-page positioning document ready to use in outreach or on a website. Use this as stage 5 (final) of the Skills-to-Business Opportunity Finder pipeline, after niche-recommender has produced its ranked shortlist, or standalone when the user asks "help me price this service" or "write a positioning statement for X".
---

# Service Packager

## Overview

Takes the top-picked niche(s) from `04-recommended-niches.md`, plus the competitor pricing signals from `03-competitors.md`, and produces the pipeline's final deliverable: a service list, tiered pricing grounded in real market pricing (not guesswork), and a short positioning document. This is the file the user takes into actual outreach or a landing page.

## Inputs

- `run_slug` (required): matches the run this continues.
- `run_date` (required): matches the run date.
- Reads `04-recommended-niches.md` for the top picks and `03-competitors.md` for pricing context.
- `niches_to_package` (optional): defaults to all top picks from stage 4; the user can narrow to just one if they've already decided.

If `04-recommended-niches.md` is missing, stop and report that stage 4's output is missing rather than guessing at the recommendation.

## Steps

1. Read `04-recommended-niches.md` for the niche(s) to package, and `03-competitors.md` for the pricing signals already gathered for those niches.
2. For each niche being packaged, define **3 service tiers** (e.g. Starter / Standard / Premium, or a one-off vs. retainer split, whatever fits the service type):
   - What's included in each tier (concrete deliverables, not vague scope)
   - Who each tier is for (buyer profile)
   - Turnaround/cadence if relevant
3. Set pricing for each tier:
   - Anchor to the real competitor pricing found in `03-competitors.md` where available (state the anchor explicitly, e.g. "competitors publish $X-$Y for comparable scope").
   - If no competitor pricing was public, use a clearly labeled estimate range based on typical freelance/agency rates for comparable scope and time investment, and mark it "estimated, no public competitor pricing found" rather than presenting it as market-verified.
   - Never present a fabricated number as if it came from real market data.
4. Write a **positioning document** (roughly half a page): a name/tagline for the service, the core promise (what problem it solves and for whom), the differentiator versus the competitors logged in stage 3, and a short "why now" line grounded in the demand evidence from stage 2.
5. Write the result to `Content/Business-Opportunities/<run_slug>/<run_date>/05-service-packages-pricing.md`:
   ```markdown
   # Service Packages & Pricing: <run_slug> (<run_date>)

   ## <Niche name>

   ### Positioning
   - Tagline: ...
   - Core promise: ...
   - Differentiator: ...
   - Why now: ...

   ### Packages
   | Tier | Included | Best for | Price | Pricing basis |
   | --- | --- | --- | --- | --- |
   | Starter | ... | ... | $... | anchored to <competitor> \| estimated |
   | Standard | ... | ... | $... | ... |
   | Premium | ... | ... | $... | ... |

   (repeat per packaged niche)
   ```
6. This file is the pipeline's final deliverable, summarizing it back to the user should reference the full chain: profile fit → demand evidence → competitive opening → recommendation → packaging, so they can see the reasoning, not just the output.

## Output

`Content/Business-Opportunities/<run_slug>/<run_date>/05-service-packages-pricing.md` — final deliverable of the pipeline (business ideas, service list, pricing, positioning document).

## Error Handling

- Never state a price as market-verified unless it's anchored to a real, cited competitor price from stage 3. Estimated prices must be labeled as estimates.
- Every positioning claim must trace back to something in the earlier stage files, not a generic template claim.
