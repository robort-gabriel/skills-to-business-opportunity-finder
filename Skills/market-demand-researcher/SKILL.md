---
name: market-demand-researcher
description: Research real-world market demand signals for a shortlist of candidate business/service niches using web search, deep research, X/Twitter discourse, and community discussion (Reddit, Facebook Groups, Quora, forums). Use this as stage 2 of the Skills-to-Business Opportunity Finder pipeline, after skill-profile-analyzer has produced its candidate niche list, or standalone when the user asks "is there demand for X service" or "how big is the market for Y".
---
# Market Demand Researcher

## Overview

Takes the candidate niches from `file 01-profile.md` (or a niche list given directly) and researches real demand signals for each: what people/businesses are actively asking for, paying for, or complaining about the lack of, in that space, including what's being said in communities like Reddit, Facebook Groups, and Quora, not just search/news/X results. Runs entirely on free built-in search tools, never a paid market-data API.

## Inputs

- `run_slug` (required): matches the run this continues, from `skill-profile-analyzer`.
- `run_date` (required): matches the run date.
- `candidate_niches` (required): the niche list, read from `file Content/Business-Opportunities/<run_slug>/<run_date>/01-profile.md` if not passed directly.

If `file 01-profile.md` is missing and no niche list was passed directly, stop and report that stage 1's output is missing rather than guessing at niches.

## Steps

1. Read `file 01-profile.md` for the candidate niche list (or use the niche list given directly).
2. For each candidate niche, gather demand signals using:
   - `web_search` (topic="news" for recent momentum, general for buyer/seller discussion) — look for phrases like "looking for", "how do I find someone to", "hire a", "need help with" tied to the niche.
   - `web_research` with `category="company"` or `category="people"` to see whether businesses are actively marketing or hiring for this niche, a sign of validated demand.
   - `x_search` for live discourse: complaints, requests, or trend spikes mentioning the niche.
3. Also check community discussion for each niche, since this is often where the most honest demand signals show up:
   - **Reddit**: `web_search`/`web_research` with queries like `site:reddit.com <niche> "looking for" OR "recommend" OR "how do I find"`, or `include_domains=["reddit.com"]`. Note the subreddit, how recent the thread is, and whether it got real replies (not just the original post).
   - **Facebook Groups**: group content itself usually isn't publicly indexed, so search for public mentions instead — e.g. `web_search` for `"facebook group" <niche>` to confirm active groups exist, and check whether businesses/creators reference driving leads from a specific FB group for this niche. Treat this as a weaker, indirect signal (group exists / is referenced) rather than being able to quote actual posts, and say so explicitly in the evidence.
   - **Quora and forums**: `web_search`/`web_research` for `site:quora.com <niche>` or niche-specific forums, looking for repeated questions asking how to find or hire for this service.
   - Skip a community platform for a niche if a genuine search turns up nothing relevant — don't force a result.
4. For each niche, note:
   - **Demand signal strength**: strong / moderate / weak / unclear, based on how many independent sources (including community sources) show active requests or hiring for it (not just general interest articles).
   - **Who's asking**: what kind of buyer (solo founders, SMBs, agencies, enterprises) shows up in the results.
   - **Community signal**: what Reddit/Facebook Group/Quora/forum activity was found, if any (subreddit/group/forum name, recency, engagement level) — or "none found" if a genuine search turned up nothing.
   - **Representative evidence**: 2-4 concrete citations (quote or paraphrase + source) backing the signal strength rating, drawing from search/news/X and community sources together. Do not rate a niche "strong" without at least 2 independent sources.
5. If a niche turns up no real demand evidence after a genuine search, mark it "unclear" rather than inventing supporting evidence, this is a valid and useful finding.
6. Write the result to `file Content/Business-Opportunities/<run_slug>/<run_date>/02-market-demand.md`:

   ```markdown
   # Market Demand: <run_slug> (<run_date>)

   ## <Niche name>
   - Demand signal strength: strong | moderate | weak | unclear
   - Who's asking: ...
   - Community signal: ...
   - Evidence:
     - <citation 1>
     - <citation 2>

   (repeat per niche)
   ```

## Output

`file Content/Business-Opportunities/<run_slug>/<run_date>/02-market-demand.md` — hands off to `competitor-scanner`.

## Error Handling

- Free-only: never call a paid market-research or SEO-data API, and never use a paid Reddit/Facebook scraping tool. Only `web_search`, `web_research`, and `x_search` against public content.
- Never fabricate a demand signal, search volume figure, quote, or community post. Every claim needs a real citation from this run's searches. If Facebook Group content can't be directly read, say so rather than inventing what was posted.