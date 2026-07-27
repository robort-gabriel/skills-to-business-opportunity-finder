<h1 align="center">Skills-to-Business Opportunity Finder</h1>

<p align="center">
  An AI agent automation workflow that turns your skills, experience, and interests into a market-validated business idea.<br/>
  Built on Zo Computer and compatible with Claude AI, it researches real demand and competitors, then hands you priced service packages and a positioning document.
</p>

<p align="center">
  <img src="https://zo.pub/robort/skills-to-business-opportunity-finder/zo-logo.png" alt="Zo Computer" width="64" /> 
</p>
<p align="center">
<img src="https://zo.pub/robort/skills-to-business-opportunity-finder/claude-logo.png" alt="Claude AI" width="64" />
</p>
<p align="center">
  <img src="https://zo.pub/robort/skills-to-business-opportunity-finder/pipeline-diagram.svg" alt="Analyze to Research to Scan to Rank to Package pipeline" width="560" />
</p>

<p align="center">
  <img alt="workflow: evidence-based" src="https://img.shields.io/badge/workflow-evidence--based-f97316" /> <img alt="cadence: on-demand" src="https://img.shields.io/badge/cadence-on--demand-7c3aed" />
</p>
<p align="center">
  <img alt="output: positioning doc" src="https://img.shields.io/badge/output-positioning%20doc-2563eb" /> <img alt="storage: Content/" src="https://img.shields.io/badge/storage-Content%2F-0891b2" />
</p>
<p align="center">
  <img alt="external APIs: none" src="https://img.shields.io/badge/external%20APIs-none-brightgreen" /> <img alt="model: Claude AI" src="https://img.shields.io/badge/model-Claude%20AI-CC785C?logo=claude&logoColor=white" />
</p>

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Folder Structure](#folder-structure)

## Overview

Most people who want to turn a skill into a business get stuck at "what should I actually sell, and for how much." This AI agent automation workflow answers that with evidence instead of guessing: it runs a five-stage pipeline that analyzes your skills, experience, and interests into candidate niches, researches whether real demand exists for each one, scans who's already competing and what they charge, ranks the niches by demand and fit, then packages the best pick into service tiers, pricing, and a positioning document. Runs entirely on free, built-in Zo Computer tools and already-connected catalog integrations, no paid market-research or SEO API required. Every skill is also compatible with Claude AI or any agentic framework, not just Zo's own routing.

## Features

| Skill | What it does |
| --- | --- |
| `skill-profile-analyzer` | Turns a free-text skills/experience/interests profile into a structured summary and 5-8 candidate niches, each traceable to something you actually stated. |
| `market-demand-researcher` | Researches real demand signals per niche via web search, deep research, X/Twitter discourse, and community discussion (Reddit, Facebook Groups, Quora); rates demand strong/moderate/weak/unclear with citations. |
| `competitor-scanner` | Finds real competitors per niche, their positioning, and any publicly visible pricing; flags each niche as crowded or underserved. |
| `niche-recommender` | Scores every niche on demand, competitive opening, and personal fit; ranks and recommends the top 2-3 with an auditable rationale. |
| `service-packager` | Turns the top pick(s) into 3 priced service tiers (anchored to real competitor pricing where available) and a one-page positioning document. |

## Requirements

- Built-in web search / research tools (`web_search`, `web_research`, `x_search`), no setup needed.
- No integration, API key, or paid market-research/SEO-data service is required or supported, this pipeline never calls a paid third-party API.

## Installation

### Fast path (recommended)

1. Open a **new Zo chat**.
2. Paste in the contents of `installation-prompt.md` and send it.
3. Zo fetches this repo, installs the skills into your project folder, offers to create a dedicated persona, and asks whether you want a one-off or recurring run, confirming with you before anything is created or scheduled.

### Manual path

1. Clone or download this repo.
2. Copy the whole project folder to `/home/workspace/Zo-Automations/Projects/skills-to-business-opportunity-finder/` on your Zo Computer.
3. (Optional) Create a persona named "Skills-to-Business Opportunity Finder" using the exact text in `persona.md`.
4. (Optional) Try it: paste a starter prompt from `starter-prompts.md` into a chat, or into the dedicated persona's chat if you created one.

### Claude AI path

The five skills (`skill-profile-analyzer`, `market-demand-researcher`, `competitor-scanner`, `niche-recommender`, `service-packager`) are plain `SKILL.md` files with no Zo-specific dependencies, so they also run under Claude AI. There are two ways to install, depending on whether "chat" means claude.ai (Cowork) or Claude Code.

#### claude.ai (Cowork)

Requires a paid plan (Pro, Max, Team, or Enterprise; Skills and code execution are gated off the Free plan).

1. Paste `installation-prompt-claude.md` into a new claude.ai chat to have Claude fetch the skill files from GitHub and zip each one individually.
2. Enable **Code execution**, **File creation**, and **Web search** in **Settings → Capabilities** (Web search substitutes for any `web_research`/`web_search`/`x_search` calls).
3. Upload each skill as its own zip under **Settings → Capabilities → Skills**, never the whole `Skills/` folder as one zip.
4. Create a Project named "Skills-to-Business Opportunity Finder" with the automation prompt as custom instructions, and `persona.md` as Project knowledge.
5. Run it by pasting your skills/experience/interests profile into a Project chat. Schedule recurring runs via Claude Cowork's Scheduled Tasks.

#### Claude Code (CLI)

1. Copy or symlink this project's `Skills/` folder into `.claude/skills/`.
2. Its native WebSearch tool replaces any `web_research`/`web_search`/`x_search` calls.
3. Run the five skills in sequence in the main thread, or as subagents.
4. Schedule recurring runs via Claude Code's Routines.

Neither sub-path needs an API key beyond your existing Claude AI access, and nothing is ever sent or published automatically on either path.

## Configuration

| Input | Required | Default | Notes |
| --- | --- | --- | --- |
| `raw_profile` | Yes | — | Free text: skills, work history, tools, interests, and constraints (time, budget, solo vs. agency). |
| `run_slug` | No | derived from name/main skill | Short kebab-case identifier used in the output folder path. |
| `run_date` | No | today (`YYYY-MM-DD`) | Used in the output folder path. |

## Usage

Run the whole pipeline in one request (see `starter-prompts.md` for more examples):

> Here's my background: [paste your skills, work history, tools, and interests]. Run the Skills-to-Business Opportunity Finder pipeline and tell me what business I should start.

Or run individual stages, e.g. just profile + demand research to sanity-check an idea before going further. Each stage reads the previous stage's output file and stops with a clear error if it's missing, no guessing at missing context.

## Folder Structure

```
skills-to-business-opportunity-finder/
├── README.md
├── installation-prompt.md
├── installation-prompt-claude.md
├── persona.md
├── automation-prompt.md
├── starter-prompts.md
└── Skills/
    ├── skill-profile-analyzer/SKILL.md
    ├── market-demand-researcher/SKILL.md
    ├── competitor-scanner/SKILL.md
    ├── niche-recommender/SKILL.md
    └── service-packager/SKILL.md
```

Outputs are written to `Content/Business-Opportunities/<run_slug>/<run_date>/`:

```
01-profile.md
02-market-demand.md
03-competitors.md
04-recommended-niches.md
05-service-packages-pricing.md
```
