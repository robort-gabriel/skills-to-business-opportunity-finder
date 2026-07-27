# Skills-to-Business Opportunity Finder — Installation Prompt

Paste everything below the line into a **new Zo chat** and send it. It's self-contained, the AI reading it has no memory of how this project was built, so it spells out every step. Swap the repo URL first if you're installing from a fork.

---

Fetch and install the "Skills-to-Business Opportunity Finder" Zo automation from this public GitHub repo:

`https://github.com/robort-gabriel/skills-to-business-opportunity-finder`

Do the following, in order. Steps marked **(confirm)** must not proceed until I explicitly approve, don't treat silence or a prior approval as blanket permission.

### 1. Fetch the repo

- Target folder: `/home/workspace/Zo-Automations/Projects/skills-to-business-opportunity-finder/`.
- **(confirm)** If that folder already exists, tell me what's in it and ask whether to overwrite before touching anything.
- Clone or download the repo (it's public, no auth needed) into that folder, preserving its structure exactly:
  ```
  README.md
  installation-prompt.md
  installation-prompt-claude.md
  persona.md
  automation-prompt.md
  starter-prompts.md
  Skills/skill-profile-analyzer/SKILL.md
  Skills/market-demand-researcher/SKILL.md
  Skills/competitor-scanner/SKILL.md
  Skills/niche-recommender/SKILL.md
  Skills/service-packager/SKILL.md
  ```

### 2. Verify the skills

- Confirm each of the five `Skills/<name>/SKILL.md` files exists and has valid frontmatter (`name` matching its folder, non-empty `description`).
- These skills are project-local by design. Do not copy them into the global `Skills/` folder or any other project — this automation only ever reads/writes inside `/home/workspace/Zo-Automations/Projects/skills-to-business-opportunity-finder/` and its output folder `/home/workspace/Content/Business-Opportunities/`.

### 3. Create a dedicated persona

- **(confirm)** the name and scope with me before creating anything.
- Read `persona.md` in the repo and use its content verbatim: the `Name` field as the persona name, the `Prompt` field as the persona's system prompt. Do not paraphrase or shorten it.
- Create the persona (via the persona-creation tool) with that exact name and prompt text.
- After creating it, ask me whether to switch to it now (set it active) or leave it available to select later.

### 4. Offer to set up recurring automation

- **(confirm)** Ask me for: `raw_profile` (required — my skills, experience, interests, and constraints), `run_slug` (optional), and whether I want this to run once or on a recurring cadence (most people only need this once per profile, so default to a one-off run unless I ask for recurring).
- Do not create a scheduled agent until I explicitly confirm I want recurring runs and give a frequency.
- Explain plainly what the automation will do (run the 5-skill pipeline and write files under `Content/Business-Opportunities/`), how often it will run (if recurring), and that each run is a full Zo session, without inventing a specific cost figure.
- If I confirm a recurring setup, create a scheduled agent using the instructions in `automation-prompt.md` (filled in with my values) as its prompt, on the frequency I gave. Otherwise, just run it once ad hoc.

### 5. Report back

- Confirm: the install path, whether the folder was overwritten or created fresh, which persona was created (and whether it's active), and whether a recurring automation was set up (with its schedule) or it was run once/left for later.
- Give me one ready-to-run example prompt from `starter-prompts.md` so I can try the pipeline right away.

Throughout all of this, do not read, write, or modify any files outside `/home/workspace/Zo-Automations/Projects/skills-to-business-opportunity-finder/` and `/home/workspace/Content/Business-Opportunities/`, and do not call any paid or external API — this automation is built to run entirely on free, built-in Zo tools and already-connected catalog integrations.
