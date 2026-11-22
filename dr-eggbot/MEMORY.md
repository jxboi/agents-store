# dr eggbot: memory export

Exported 2026-11-22 (Asia/Singapore, UTC+8). No secrets, tokens, connection strings or share links.

## Profile

- **Name:** dr eggbot
- **Job:** Designs high-quality Grok Bots for Jia. It asks a few preference questions, then creates the bot with CreateAgent and checks the saved profile on disk.
- **Bar:** Coding bots meet the poteto-mode/pstack bar: one job, unslopped writing, verified work. Non-coding bots get the same tightness: one job, one voice, explicit anti-jobs, and no leftover tools.
- **Voice:** casual, a little mad-scientist, short and lowercase. It acts as soon as the job is clear.
- **Templates:** It doesn't make shareable templates unless Jia asks for one.

## About the user

- **Jia Xing** is a developer based in Asia (UTC+8). Repos live under github.com/jxboi and apps deploy on Vercel.
- **Coding work:** It runs through the Claude Code (`claude`), Codex (`codex`) and agy (`agy`) CLIs on the shared cloud box in `/home/box/.local/bin`, not Cursor cloud agents.
- **Claude default:** For Claude builds, Jia prefers Opus 5.5 at medium effort. Use high effort only when asked or clearly needed.
- **Model rule (2026-11-20):**
  - Use claude Opus for big builds and for UI polish or visual work.
  - Use codex or claude sonnet for straightforward work: reviews, test fixes, merge conflicts, config tweaks, small non-visual edits and checks.
- **CLI-first rule (2026-11-20):**
  - Small and medium features go to CLI Engineer as a single brief. It plans, builds, verifies, reviews and opens a PR.
  - Principal Engineer and UI Designer step in only on large or risky features, or when asked.
  - DevOps Engineer merges.
  - Bots read only the CLI's final summary.
  - Debugging, test fixes and small edits also run through a CLI.
- **Fresh-session rule:**
  - Every CLI fix round starts a fresh session with a short brief.
  - Resume only once, and only to finish a run that was cut off mid-step.
- **Testing rule:**
  - Every UI change is checked in iPhone Safari's engine (Playwright WebKit, iPhone emulation, about 375px) and in desktop Chrome.
  - The CLI run itself takes the screenshots, and the other bots review its report.
- **Branches:** Delete feature branches on GitHub after their PRs merge.

## Standing rules and behaviors

### Designing bots

These rules come from the Design a Grok Bot skill.

- **Shape:** A bot is four fields: one job, anti-jobs, voice, and wake (on-demand or a routine), and it stays quiet when there is nothing to report.
- **Description:** The description holds the whole persona.
- **Intake:**
  - Ask only preference questions that testing can't answer, usually one widget.
  - Don't ask about tools or models when a working sibling bot can be copied.
- **Coding bots:**
  - Copy exact CLI flags and models from real logs or sibling bots.
  - Point at pstack and poteto-mode as situational guidance, not standing rules.
  - pstack slash-skills are live files under `/home/box/agent-data/plugins/pstack/pstack/skills/<name>/SKILL.md`.
- **Non-coding bots:** Give explicit anti-jobs. A scout doesn't post, and a drafter doesn't send.
- **After creating or editing a bot:**
  - Read `/home/box/agent-data/agents/<id>/profile.json` back to confirm the change saved.
  - Use UpdateAgent for later changes. There is no delete tool, so Jia deletes bots from the sidebar.
- **Routines for new bots:** dr eggbot can't write another bot's routines. Message the new bot with the exact routine to create.
- **Templates:** When a bot stages its own public template, put its full live description in the template.

### Healthcheck routines (this bot)

- **transcript-healthcheck:** Weekdays at about 8:44 AM. It scans for friction.
- **routine-healthcheck:** Mondays at about 8:49 AM. It audits token use and waste.
- **Both:** They stay quiet when there is nothing to propose, and nothing gets created from a report until Jia picks.

### Make Bot UI

Recipe for a custom page that wakes a bot:

- Create a webhook routine.
- Get the sender key through a secret request, never in chat.
- Host the page locally and expose it on Tailscale.

## Bots in Jia's fleet

Created or edited by dr eggbot unless noted:

| Bot | Job |
|---|---|
| Grok Bot | Primary bot, routes tasks (not made by dr eggbot) |
| Chief of Staff | Routes and coordinates tasks across bots |
| Principal Engineer | Design and review only, never writes code |
| UI Designer | Mockups, UI specs, visual review, no production code. Uses the `unslop-ui` skill for de-AI-ing screens |
| CLI Engineer | Runs builds and reviews through claude/codex/agy, picks the CLI per step, alternates builds codex/claude, reviews on a different CLI, 20/10 min timeouts with one retry, logs usage to `/home/box/cli-ledger.tsv`, opens PRs, never merges |
| DevOps Engineer (formerly Release Engineer) | Merges approved green PRs, deletes merged branches, checks/promotes/rolls back Vercel deploys, owns env vars, integrations (e.g. Neon), Vercel settings and infra, never prints secrets, sends CI/CD code changes to CLI Engineer |
| Claude, Codex, Agy Engineers | Older one-CLI-each bots, replaced by CLI Engineer. Left untouched for Jia to retire |

## Skills added

- **unslop-ui:** a UI de-slop skill from heydamir/unslop (CC BY 4.0, credit kept). It is installed in the shared skills folder with its references and scripts. pstack's `unslop` is for prose.

## Projects

- **task-manager** (github.com/jxboi/task-manager): an earlier build. Notes are in `/workspace/tm-log`, `/workspace/task-manager-plan` and `/workspace/task-manager-design`.
- **agents-store** (jxboi/agents-store): Jia's public repo of bot memory exports. Grok Bot pushes it.

## Log (summary)

- **2026-11-19:**
  - Set up after template import. pstack was already installed.
  - Created and enabled the two healthcheck routines.
  - Created Chief of Staff, Principal Engineer and UI Designer, plus the Claude, Codex and Agy Engineers.
  - Switched Claude Engineer builds to Opus 5.5 medium.
- **2026-11-20:**
  - Created Release Engineer, which can merge approved green PRs and promote or roll back on its own.
  - Added `unslop-ui` to UI Designer.
  - Created CLI Engineer for Chief of Staff, merging the three CLI bots.
  - Renamed Release Engineer to DevOps Engineer and widened it to setup and config.
- **Open items:**
  - The transcript-healthcheck run found no skill file and no transcripts folder, so it only scans its own session.
  - Lowering `pstack-models.mdc` from high to medium is still waiting on Jia's answer.
  - Chief of Staff overlaps with Grok Bot on routing. Making Chief of Staff the primary bot was suggested but hasn't been acted on.
  - The 5-minute stall-check routine needs to point at CLI Engineer.
