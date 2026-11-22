# Grok Bot memory export

This is Grok Bot's memory for Jia Xing, exported on 2026-11-22. All times are UTC+8. It contains no secrets.

## Role
- I'm Jia's primary bot. I take any task and route it to the right one of his other bots.
- In practice, most of my work arrives from Chief of Staff, and since 2026-11-20 also from DevOps Engineer. These requests are mostly GitHub housekeeping on `jxboi/task-manager` that their own tools can't do.
- I reply to the bot that sent the request, and tell Jia the result in a short message.

## About Jia
- His name is Jia Xing, his GitHub username is `jxboi`, and he's in UTC+8.
- He uses Grok Bot mainly for development work.
- He pays for Claude Code, OpenAI (Codex) and Antigravity (agy).
- The `claude`, `codex` and `agy` CLIs are installed in `/home/box/.local/bin` on the shared box and signed in with his subscriptions.

## Standing rules and behaviors
### Coding through CLIs
- All coding goes through the CLIs (`claude`, `codex`, `agy`).
- Bots hand work to a CLI in one brief and read only the CLI's final summary, not code, diffs or full logs.
- Debugging, test fixes and small edits also go through a CLI run.
- Small and medium features go to CLI Engineer in one brief. Principal Engineer and UI Designer step in only on large or risky work or when asked.
- The CLI run does its own browser checks and screenshots and writes a short report. Other bots review that report and those screenshots.

### Running CLI steps
- Each fix round starts a fresh CLI session, not `--continue` or resume. The exception is resuming once to finish a run that was cut off mid-step.
- Use Claude Opus for big builds and anything visual or UI polish. Use Codex or Claude Sonnet for straightforward work like reviews, test fixes, conflict merges, config tweaks and checks.
- The shared box pauses when no bot has an active turn. So every CLI step gets a hard timeout (about 20 minutes for builds and 10 for reviews) and one automatic retry on a timeout or failure.
- Steps expected to take under about 10 minutes run in the foreground within the same turn, never backgrounded with the turn ended.

### Testing and reporting
- Every UI change is verified in iPhone Safari's engine (Playwright WebKit with iPhone emulation, about 375px wide) as well as desktop Chrome.
- Build reports stay short and include real CLI token and cost numbers from the logs, plus wall time. Any estimate is labeled as one.

### Who does what
- DevOps Engineer (formerly Release Engineer) owns merges and all setup: Vercel env vars, integrations and repo settings. I don't do those unless Jia asks me directly.
- I still delete merged branches when asked, because DevOps Engineer's GitHub connector can't.
- Jia wants feature branches deleted after their PRs merge. Before deleting one, I confirm the PR shows as MERGED with the expected merge commit, delete only that branch, and list the remaining branches afterward.

### Security
- Never print, echo or post tokens, connection strings or secret values.
- Pass secrets to tools by file reference, so I never see them.
- Keep Vercel share links out of commits, PR bodies and logs.
- Don't change the Vercel project's protection settings or Neon Auth.

### Sends
- Pushing commits to `jxboi/agents-store` is a saved allowed action.

## Bots I work with
- **Chief of Staff:** takes Jia's tasks and routes them to a bot. This is my main source of requests.
- **DevOps Engineer:** merges, deploys and setup.
- **CLI Engineer:** builds and reviews through the CLIs.
- **Claude Engineer, Codex Engineer and Agy Engineer:** each runs one CLI.
- **Principal Engineer:** design and review.
- **UI Designer:** design and visual review.
- **dr eggbot:** creates new bots.

## Projects
### jxboi/task-manager
- Jia's web app, deployed on Vercel. The server and database are in the iad1 (Washington) region.
- Database: Neon Postgres (neon-task-manager, Free plan), added 2026-11-20, with Neon Auth enabled.
- Sign-in: Better Auth.
- Pushes use a fine-grained GitHub token kept on the box. On 2026-11-22 Jia widened it to all of his repos.
- The token can't change repo settings. The delete-branch-on-merge setting needs Jia or Admin permission.

### jxboi/agents-store
- A public repo holding the bots' memory exports.
- Chief of Staff's export was pushed on 2026-11-22 as commit 7badb31.
- A combined push of every bot's folder is pending Chief of Staff's go-ahead.

## Log (summary)
- **2026-11-19:** Set up the CLIs on the box and recorded Jia's coding-via-CLI preferences.
- **2026-11-20:**
  - Merged PR #3 (reminders) and deleted its branch, before the rule that DevOps Engineer owns merges arrived.
  - Fixed the reminders browser-check script to match the spec. Production passed 16 of 16.
  - Tried to turn on auto-delete of merged branches, but the token lacked permission (HTTP 403).
  - Jia created the Neon database himself. I added the BETTER_AUTH_SECRET and BETTER_AUTH_URL env vars and a local, git-ignored `.env.neon`.
  - Deleted the merged branches of PRs #4, #5, #6, #7, #8, #9, #10 and #11.
  - Reviewed CLI usage for PR #5, but Jia stopped me before I reported it.
- **2026-11-21:** Deleted the merged branches of PR #12 (chore/migration-check) and PR #13 (feat/ui-redesign) for DevOps Engineer. Since then, `main` has been the only branch on task-manager.
- **2026-11-21 to 2026-11-22:**
  - My push of Chief of Staff's export to agents-store was refused (HTTP 403) because the token covered only task-manager.
  - Jia widened the token, and I pushed the export as 7badb31.
  - The repo's visibility was left public, as Jia didn't ask to change it.
- **2026-11-22:** Wrote this export, holding the push until all 9 bots' exports are in.
