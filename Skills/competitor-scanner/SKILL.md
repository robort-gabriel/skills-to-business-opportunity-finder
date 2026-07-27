---
name: competitor-scanner
description: Identify real competitors and existing providers for each candidate niche, along with their positioning and any publicly visible pricing signals. Use this as stage 3 of the Skills-to-Business Opportunity Finder pipeline, after market-demand-researcher has produced its demand-signal file, or standalone when the user asks "who else is offering this service" or "what's the competition like for X".
---

# Competitor Scanner

## Overview

Takes the niches from `02-market-demand.md` and, for each one, finds real businesses/freelancers already offering that service: who they are, how they position themselves, and any pricing that's publicly visible (rate cards, package pages, marketplace listings). This grounds the eventual recommendation in what the market will actually bear, not guesswork.

## Inputs

- `run_slug` (required): matches the run this continues.
- `run_date` (required): matches the run date.
- Reads `Content/Business-Opportunities/<run_slug>/<run_date>/02-market-demand.md` for the niche list.

If `02-market-demand.md` is missing, stop and report that stage 2's output is missing rather than guessing at the niche list.

## Steps

1. Read `02-market-demand.md` for the niche list (skip niches already marked "unclear" with no evidence unless the user asks to scan them anyway, weak demand usually means weak competitor scanning ROI too).
2. For each remaining niche, search for existing providers using:
   - `web_research` with `category="company"` to find agencies/businesses offering the service.
   - `web_search` for freelance marketplace presence (e.g. "hire a <niche> freelancer") and directory listings.
   - `x_search` to catch independent operators/solopreneurs who market on X but may not have a dedicated marketing site.
3. For each niche, log 3-6 representative competitors (skip if genuinely fewer exist, don't pad the list) with:
   - **Name/handle** and what they offer, in their own words where possible.
   - **Positioning angle**: how they differentiate (speed, price, niche specialization, full-service vs. productized, etc.)
   - **Pricing signal** (if publicly visible): exact price/range if published, or "not published" if not. Never estimate a competitor's price without a public source.
4. Summarize per niche: is this crowded (5+ well-established competitors, saturated positioning) or underserved (few competitors, or existing ones cluster around one positioning angle leaving others open)?
5. Write the result to `Content/Business-Opportunities/<run_slug>/<run_date>/03-competitors.md`:
   ```markdown
   # Competitor Scan: <run_slug> (<run_date>)

   ## <Niche name>
   - Market read: crowded | underserved | moderate
   - Competitors:
     - **<Name>** — offers: ... | positioning: ... | pricing: <published price or "not published">
     - ...

   (repeat per niche)
   ```

## Output

`Content/Business-Opportunities/<run_slug>/<run_date>/03-competitors.md` — hands off to `niche-recommender`.

## Error Handling

- Never invent a competitor, their positioning, or a price they haven't actually published. If pricing isn't public, say so, don't estimate it as fact (a clearly labeled estimate range is fine only if flagged as such).
- Free-only: only `web_search`, `web_research`, `x_search`. No paid competitive-intelligence API.
