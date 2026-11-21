# Chief of Staff: memory export (2026-11-21)

Exported from Chief of Staff's memory for Jia Xing (UTC+8). No secrets are included.

## Role
Chief of Staff routes Jia's tasks to teammate bots with a self-contained brief (goal, context, done-when), tracks them, and reports back. It does no coding, research or outside messaging itself.

## User profile
- The user's name is Jia (Jia Xing), a developer in Asia/Taipei (UTC+8). GitHub username: jxboi.
- Jia uses Grok Bot mainly for development work and designs Grok Bots directly.
- Jia has paid subscriptions to Claude Code, OpenAI and Antigravity.
- Claude Code (`claude`), Codex (`codex`) and agy (`agy`) CLIs are installed in ~/.local/bin, on the bots' shared cloud computer and on Jia's computer, signed in with Jia's subscriptions. Jia wants coding done through these CLIs.

## Standing rules
- **Usage-cut rule (2026-11-21):** Chief of Staff routes only new or multi-bot work. CLI Engineer, UI Designer and DevOps Engineer report straight to Jia, and Jia messages them directly for small fixes, tweaks and merge approvals. DevOps deletes branches itself. Each bot keeps Jia's standing rules in its own instructions, so briefs state only goal, context and done-when. Log only decisions and finished work.
- **CLI-first (2026-11-20):** Bots hand work to a CLI with one brief and read only the CLI's final summary, not code, diffs or full logs. Debugging, test fixes and small edits also go through a CLI. The CLI run does its own browser checks and screenshots and writes a short report; other bots review that report.
- **Dev workflow (2026-11-20):** Collect Jia's decisions in one card. Small and medium features go as one brief to CLI Engineer (plan, build, self-verify with screenshots, CLI review, PR). Large or risky features add Principal Engineer planning and UI Designer design via CLI first. DevOps Engineer merges, deletes the branch and checks prod.
- **Model rule (2026-11-20):** Opus for big builds (multi-layer features, new data models or migrations, cross-cutting changes, more than about 5 files, anything needing a plan) and for any UI polish or visual work however small. codex or claude sonnet for straightforward work (review or test fixes, conflict merges, config tweaks, small non-visual edits, checks).
- **Fresh-session rule (2026-11-20):** Every CLI fix round starts a fresh session with a short brief, never --continue or resume, except resuming once to finish a run cut off mid-step.
- **iPhone Safari testing (2026-11-20):** Every UI change is verified in Playwright WebKit with iPhone emulation (about 375px, iPhone 14) as well as desktop Chrome.
- **Stay-in-turn (2026-11-20):** CLI steps expected under about 10 minutes run in the foreground and are followed up in the same turn.
- **CLI freeze (2026-11-20):** The shared computer pauses when no bot has an active turn. Every CLI step gets a hard timeout plus one auto-retry. The `cli-keep-awake-check` routine (every 5 min) is resumed when a build or review starts and paused when no CLI runs.
- **Reviews (2026-11-20):** No hard cap on reviews; issues get fixed. **Update 2026-11-21:** rare edge-case races are listed as follow-ups instead of looping on review (Jia shipped PR #14 with 3 such findings skipped).
- **Lean usage (2026-11-20):** Skip UI Designer's full visual review on small PRs. Chief of Staff routes only, with short updates, and doesn't relay every bot message.
- **Branches:** Delete a PR's feature branch once it merges. Jia was asked to enable GitHub "Automatically delete head branches" on jxboi/task-manager (not yet confirmed).
- **Merges:** DevOps merges only the head SHA Jia approved; a changed head needs re-approval.

## Teammate bots
- **CLI Engineer** (405687ec-10b3-4c52-9bee-abcb8c3a5cf0, created 2026-11-20): default for coding builds and CLI reviews. Picks claude, codex or agy and balances quota between them. Logs to /home/box/cli-ledger.tsv. Opens PRs, never merges. It replaced Claude Engineer, Codex Engineer and Agy Engineer (Jia was asked to delete them).
- **DevOps Engineer** (9e95899f-9c8f-49d1-98c5-0c63d9f199c1, called Release Engineer until 2026-11-20): PR merges, branch cleanup, prod deploy checks, and all setup and config (env vars, integrations, project settings, infra). Asks Jia only before destructive steps.
- **Principal Engineer:** architecture plans and reviews for large or risky work.
- **UI Designer:** mockups, UI specs and visual review.
- **Grok Bot:** primary bot for one-off and repo work.
- **dr eggbot:** designs and creates new bots.

## Workstream: task-manager
- Jia's web app at [jxboi/task-manager](https://github.com/jxboi/task-manager), deployed on Vercel at https://task-manager-mu-sepia-18.vercel.app. A small project, so keep token and CLI cost down.
- Neon Postgres (Free plan), added 2026-11-20 through Vercel for Preview and Production (they share one DB). Jia manages the Neon DB; DevOps handles env and deploy setup. Production builds apply pending migrations automatically (since PR #12).
- The server and DB are in the Washington region (iad1), decided 2026-11-20. The old Vercel project task-manager-s25s was deleted.

### History
- 2026-11-19: Todo app plan and design, then PR #1 merged; branch deleted.
- 2026-11-20: Tags (inline #tags, OR multi-tag filter, per-tag colors), PR #2 merged.
- 2026-11-20: Reminders (date and time per todo, browser notification plus in-app highlight, daily and weekly repeats, overdue sorted to top), PR #3 merged as d30b277. PR #4 (iOS date field) merged as e2381da. PR #5 (overdue card polish) merged as ea85046.
- 2026-11-20: Neon plus sign-in (Better Auth email/password, DB sessions, per-user scoping, versioned SQL migrations), in two PRs. PR #6 merged as 9542432, PR #7 (preview Origin fix) as 583aa54, PR #8 (server storage) as fdbbf8b. PR #9 (region sin1 to iad1) merged as 41d7d7e.
- 2026-11-20: PR #10 (recurring-complete fix) merged as e857cad. PR #11 (edit task) merged as 42dc0b5. Prod then broke because migration 0003 was never applied; it was rolled back to dpl_HmspbtwY.
- 2026-11-21: PR #12 (release migration check; builds apply migrations) merged as 2656ca8; 0003 applied and prod restored.
- 2026-11-21: Full iPhone 14 redesign (paper-planner look, grouped reminder picker, tag-tap filtering removed, no helper text), PR #13 merged as a279d73.
- 2026-11-21: List tweaks (circle checkbox, no dividers, + button by Tasks title, profile menu, counts and clock icon removed), PR #14 merged as cdbd3e0, with 3 skipped edge findings as follow-ups.
- 2026-11-21: Drag-to-reorder plus iOS keyboard fix, PR #15 merged as 3d64d75; migration 0004_todo_position applied. A real-iPhone check of the keyboard fix is pending.
- 2026-11-21: Preview-only demo login, PR #16 (head a4b4b50) open and green; the hosted-Preview demo sign-in check is pending.

### Open items (2026-11-21)
- Jia to merge-approve PR #16 after the hosted-Preview check.
- Jia to check the keyboard fix on his real iPhone.
- Jia to enable GitHub auto-delete for head branches; feat/list-tweaks and feat/reorder-tasks are still undeleted.
