# Skills-to-Business Opportunity Finder — Installation Prompt (claude.ai)

Paste everything below the line into a **new claude.ai chat** and send it. It's self-contained, the AI reading it has no memory of how this project was built, so it spells out every step. Swap the repo URL first if you're installing from a fork.

This path is for claude.ai (Cowork), not Claude Code. It requires a plan with Skills and code execution enabled (Pro, Max, Team, or Enterprise). Before sending this prompt, go to **Settings → Capabilities** and turn on **Code execution**, **File creation**, and **Web search**, they're required for the steps below to work.

---

Help me install the "Skills-to-Business Opportunity Finder" automation from this public GitHub repo:

`https://github.com/robort-gabriel/skills-to-business-opportunity-finder`

Do the following, in order. Steps marked **(confirm)** must not proceed until I explicitly approve, don't treat silence or a prior approval as blanket permission.

### 1. Fetch the five skills

- Using web search / fetch, retrieve the raw contents of these five files from the repo:
  ```
  Skills/skill-profile-analyzer/SKILL.md
  Skills/market-demand-researcher/SKILL.md
  Skills/competitor-scanner/SKILL.md
  Skills/niche-recommender/SKILL.md
  Skills/service-packager/SKILL.md
  ```
- Confirm each file has valid frontmatter (`name` matching its skill folder, non-empty `description`). If any file can't be fetched or looks malformed, stop and tell me which one and why, rather than guessing its contents.

### 2. Package each skill as its own zip

- Using code execution, create five separate folders (one per skill name above), each containing only that skill's `SKILL.md`, then zip each folder individually.
- Skills must be uploaded to claude.ai as one zip per skill, never the whole set as a single zip. Give me all five `.zip` files to download.
- Tell me plainly: I still need to go to **Settings → Capabilities → Skills** myself and upload each zip, then toggle it on, that part can't be done from inside a chat.

### 3. Fetch the instruction files

- Fetch the raw contents of:
  ```
  persona.md
  automation-prompt.md
  starter-prompts.md
  ```
- Turn `persona.md` into a downloadable file exactly as fetched (I'll upload this as a Project knowledge file myself).

### 4. Draft the Project custom instructions

- Using `automation-prompt.md`'s content (objective + steps) and `persona.md`'s prompt text, draft a single combined custom-instructions text suitable for pasting into a claude.ai Project's custom instructions field. It should describe: the five-stage pipeline (`skill-profile-analyzer` → `market-demand-researcher` → `competitor-scanner` → `niche-recommender` → `service-packager`), that research stages only use web search (Web search substitutes for `web_search`/`web_research`/`x_search`, none of this pipeline ever calls a paid market-research or SEO-data API), and that no skill, demand signal, competitor, or price may be fabricated (estimated prices must be labeled as estimates, not presented as market-verified).
- Show me the drafted text before I use it. Don't shorten or drop the no-fabrication rule, it's load-bearing.

### 5. Guide me through creating the Project

- Tell me the exact manual steps: create a new Project named "Skills-to-Business Opportunity Finder", paste in the custom instructions from step 4, and upload `persona.md` (from step 3) as a Project knowledge file.
- Explain that chats inside this Project will then have the pipeline logic and skills in scope automatically, and that file creation inside a Project chat is chat-scoped, not a persistent folder tree like the Zo version, so I'll need to download outputs I want to keep.
- Explain that a run starts by pasting my skills/experience/interests profile directly into a Project chat, there's no separate config file to fill in first.

### 6. Offer a scheduled run

- **(confirm)** Ask me whether I want a recurring run via Claude Cowork's Scheduled Tasks (most people only need this once per profile, so confirm before setting up anything recurring), and if so, what frequency and whether I want a run summary or just saved output files.
- Explain plainly that Scheduled Tasks run in the cloud on the schedule I set, using the same instructions from `automation-prompt.md`.
- Since Scheduled Tasks are set up through claude.ai's own scheduling UI rather than from inside a chat, give me the exact task description text to paste in when I create it there.

### 7. Report back

- Confirm: which files were fetched successfully, the five zip files are ready for me to download and upload manually, the drafted Project custom instructions, and whether I want to set up a Scheduled Task (and its frequency/notify preference) or just run it once now.
- Give me one ready-to-run example prompt from `starter-prompts.md` so I can try the pipeline once the Project is set up.

Throughout all of this, never fabricate a skill, demand signal, competitor, or price, never call a paid market-research, competitive-intelligence, or SEO-data API (only Web search), and always label estimated prices as estimates, never as market-verified data.
