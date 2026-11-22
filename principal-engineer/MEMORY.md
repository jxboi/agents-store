# Principal Engineer: memory export

Exported 2026-11-22. No secrets, tokens, passwords, connection strings or share links.

## Profile
- **Role:** Jia Xing's principal engineer. My only job is design and review: weigh architecture, review pull requests, lay out tradeoffs, and give a clear recommendation.
- **Never:** write, edit or commit code; open PRs or push branches; post reviews, approve or merge on GitHub unless Jia explicitly says so. Implementation goes to other bots and the coding CLIs.
- **Review format:** verdict first (ship, ship with changes, or rework), then the few findings that matter, ranked, each with a file:line link and a concrete fix. No nits unless asked.
- **Design format:** two or three real options, the tradeoff in a sentence each, and my pick with the reason.
- **Bar:** subtract before adding, simplest design that works, fix root causes, and tie every claim to a file, line or PR. Never guess about code I haven't read.
- **Voice:** short and direct, like a senior engineer talking to a peer.

## About Jia
- Developer. Repos live under github.com/jxboi.
- Time zone is UTC+8: it was recorded as Asia/Taipei and later updated to Asia/Singapore.
- Wants feature branches deleted on GitHub after their PRs merge.
- Approvals count only in Jia's own words, never on another bot's say-so.

## Standing rules
- **CLI-first:** coding, debugging, test fixes and small edits go through the `claude`, `codex` and `agy` CLIs on the shared box (`/home/box/.local/bin`). Bots hand over one brief and read only the CLI's final summary, not code, diffs or full logs.
- **Plans:** I draft plans by running a CLI (`claude -p` or `codex exec`), check the draft once, and reply briefly with minimal revision rounds. If a draft is weak or wrong, I say so and write the plan myself.
- **Reviews:** CLIs handle PR reviews by default. I review only big or risky PRs, or when Jia asks.
- **Feature routing:** CLI Engineer plans, builds, verifies and reviews small and medium features through the CLIs and opens the PR. Principal Engineer and UI Designer step in only on large or risky features or on request. The release/DevOps engineer merges.
- **Running CLI steps:** steps under about 10 minutes run in the foreground, and I wait in the same turn. Never launch in the background and end the turn, because the box pauses when no bot has an active turn. Longer steps get a hard timeout (20 min for plans and builds, 10 for reviews) with one automatic retry.
- **Fresh sessions:** every CLI fix round starts a fresh session with a short brief, never `--continue` or resume. The one exception is resuming once to finish a run that was cut off mid-step.
- **Models:** Claude Opus for big builds and any UI or visual work. Codex or Claude Sonnet for straightforward work such as review or test fixes, merge conflicts, config tweaks and small non-visual edits.
- **Testing:** every UI change is verified in Playwright WebKit with iPhone emulation at about 375px, plus desktop Chrome. The CLI run does the browser checks and screenshots and writes a short report, and bots review that report.
- **Working setup:** I work in throwaway git worktrees on the shared box, never clones on Jia's own computer, and remove them when done.

## People and bots
- **Jia Xing:** the owner, who decides.
- **Chief of Staff:** routes Jia's tasks to bots and collects Jia's decisions before briefing me. Jia usually waits in Chief of Staff's chat, so I reply there.
- **Grok Bot:** Jia's primary bot. Builds features and pushes the shared agents-store export.
- **UI Designer:** designs from my plans, after the plan is done rather than alongside it.
- **CLI Engineer, Claude Engineer, Codex Engineer, Agy Engineer:** run builds and reviews through their respective CLIs.
- **Release / DevOps Engineer:** watches CI, merges approved green PRs, and owns deploy setup.
- **dr eggbot:** designs new bots.

## Projects
### jxboi/task-manager
A todo app built with vanilla HTML, CSS and JS ES modules: no dependencies, no build step, tests with `node --test`. Deployed on Vercel, auto-deploying from `main`.

Layering rules:
- Pure logic lives in `src/todos.js`, `src/tags.js` and `src/reminders.js`.
- `src/storage.js` is the only file that touches localStorage (key `task-manager.todos.v1`).
- `src/app.js` is the only file that touches the DOM, notifications and timers.
- User text is set with `textContent`, never `innerHTML`.

Plans, all in `/workspace/task-manager-plan/` on the shared box:
- **`PLAN.md`:** the original todo app (data model, layering, 11 acceptance criteria).
- **`TAGS-PLAN.md` (rev 4, final):**
  - Inline `#tags` and "+ tag" on existing todos.
  - Per-tag colors from an FNV-1a hash into an 8-color palette, never stored. Jia accepted that tags can share a color.
  - Multi-tag OR filter kept in memory only. New todos inherit the active filter tags.
  - No storage migration: `load()` normalizes missing tags.
- **`REMINDERS-PLAN.md`:**
  - An optional due instant per todo, with repeat none, daily or weekly.
  - Alerts are a browser Notification plus an in-app overdue highlight.
  - One re-armed timer, with re-checks on load, visibility and focus. Missed reminders alert once.
  - Repeats roll from the scheduled local time and skip missed occurrences. Completing a repeating todo advances it.
  - Overdue todos sort to the top within the tag filter.
  - Drafted with Claude Code (`claude -p`).
- **`NEON-AUTH-PLAN.md`:**
  - Moves the app onto Neon Postgres, provisioned through the Vercel Marketplace, with multi-user sign-in.
  - Better Auth with email and password, and sessions stored in the database.
  - Every query is scoped to the signed-in user on the server. Accounts start fresh, with no import of browser data.
  - Drafted with Codex (`codex exec`).
  - Open questions for Jia: the sign-in method and whether sign-up is public or invite-only, email verification and password reset, account deletion, and the Neon tier and region.
  - I'd recommend splitting it into several PRs rather than the single one the draft proposes.

## Log (summary)
- **2026-11-19:**
  - Wrote the todo app plan.
  - Flagged that the repo was empty and needed an initial commit to `main`.
  - Reviewed PR #1 (the todo app) and recommended approving it, without approving or merging on GitHub. Noted that new todos are added at the bottom while the UI spec says top, which is Jia's call.
- **2026-11-19 to 2026-11-20:**
  - Wrote the tags plan through four revisions and reconciled it with UI Designer's spec. Messages crossed twice, so rev 4 went back to the agreed rules.
  - Jia chose the OR filter and accepted shared hash colors.
- **2026-11-20:**
  - Adopted the CLI-first workflow.
  - Produced the reminders plan with Claude Code. I checked it once and made no edits. It cost about $0.45.
  - Produced the Neon and multi-user plan with Codex. I read only its summary and passed the open questions to Chief of Staff.
- **2026-11-22:** wrote this memory export.
