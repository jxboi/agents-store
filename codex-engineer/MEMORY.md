# Codex Engineer: memory export

Exported 2026-11-22 (Asia/Singapore, UTC+8). No secrets included.

## Role
Jia Xing's Codex engineer. Launches and supervises the `codex` CLI (`/home/box/.local/bin/codex`) on the bots' shared cloud computer for coding, debugging, verification and review. Verifies the real output (exit code, git status and diff, test results, token counts from Codex session logs) and reports back. Never launches `claude`, `agy` or Cursor cloud agents. Never merges PRs. Never posts externally unasked.

## About the user
- Name: Jia Xing. GitHub: `jxboi`. Time zone: UTC+8 (Asia/Singapore, earlier recorded as Asia/Taipei).
- Repos live under github.com/jxboi.
- Wants feature branches deleted on GitHub after their PRs merge.
- Wants coding work done through the `claude`, `codex` and `agy` CLIs on the shared box, never cloned onto Jia's own machine.

## Standing rules
- Hard timeouts: wrap every CLI step in a hard timeout (about `timeout 20m` for builds, `timeout 10m` for reviews). Retry once automatically on timeout or non-zero exit, and keep steps short. The shared box pauses when no bot has an active turn, which can leave runs hanging.
- Fresh sessions: every fix round (review fixes, test fixes, follow-up edits) starts a fresh CLI session with a short brief. Never use resume or continue, except to resume once and finish a run cut off mid-step.
- CLI-first: bots hand work to a CLI with one brief and read only its final summary, not the code, diffs or full logs. Debugging, test fixes and small edits also go through a CLI run.
- CLI-first: small and medium features go in one brief to CLI Engineer, which plans, builds, verifies, reviews and opens the PR. Principal Engineer and UI Designer step in only on large or risky features. Release Engineer (now DevOps Engineer) merges.
- CLI-first: the CLI run does its own browser checks and screenshots and writes a short report. Other bots review that report.
- Models: claude Opus for big builds and UI or visual polish. codex or claude sonnet for straightforward work like review fixes, test fixes, conflict merges, config tweaks and small non-visual edits.
- Testing: every UI change is verified in Playwright WebKit with iPhone emulation (about 375px wide) as well as desktop Chrome.
- Shipping: branch from `main`. Never commit to `main` and never merge PRs. Push from the box with environment tokens and never echo secrets.
- Sandboxes: `-s read-only` for reviews and audits, `-s workspace-write` for coding, and full bypass only when local servers, headless Chrome or git push need it. Never edit a directory another CLI is modifying at the same time.
- Reporting: lead with the outcome, the PR or commit, the checks that passed, and the logged CLI tokens (uncached input, cached input, output). Codex logs no dollar cost.

## Codex invocation pattern
`timeout 20m codex exec -m <model> -c model_reasoning_effort="<effort>" -s <sandbox> -C <dir> -o <last_msg_file> - < prompt.md > out.log 2> out.err`, run in the background with one retry loop. Runs live under `/workspace/codex-runs/<name>/`. Token usage comes from `~/.codex/sessions/YYYY/MM/DD/rollout-*.jsonl`.

Models: `gpt-6.2-sol` by default (medium or high effort), `gpt-6.2-astra` for hard architecture or bugs, `gpt-6.1-terra` for visual checks, `gpt-6-luna` for fast simple tasks.

## Environment notes (as of 2026-11-20)
- codex-cli 0.170.0 is installed and logged in with ChatGPT.
- The GitHub connector is linked as `jxboi`. The `gh` CLI is not logged in, but git push over HTTPS works from the box.
- pstack skills: `/home/box/agent-data/plugins/cache/cursor-public/pstack/<rev>/skills/<name>/SKILL.md`.

## Bots
- Chief of Staff routes Jia's tasks and sends me briefs.
- Grok Bot is the primary bot, and it pushes the agents-store exports.
- Principal Engineer handles design and PR review.
- UI Designer owns design specs, for example `/workspace/task-manager-design/`.
- Claude Engineer and Agy Engineer are the sibling CLI supervisors.
- CLI Engineer runs builds and reviews through all three CLIs.
- DevOps Engineer (formerly Release Engineer) merges approved green PRs and owns deploys.
- dr eggbot designs new bots.

## Projects
- jxboi/task-manager, local checkout at `/workspace/task-manager`. PR #2 (tags) is merged. PR #3 (`feature/reminders`, reminders with due times, repeats and notifications) is open.

## Log
- 2026-11-20 07:37: First run. Checked Codex install and login, GitHub access and pstack paths.
- 2026-11-20 10:17: Chief of Staff asked me to align the reminder editor's empty-date behavior on PR #3 with UI Designer's spec. Codex (`gpt-6.2-sol`, medium effort) found it did not match and fixed it.
- 2026-11-20 11:04: Pushed commit `b55dd4a` to `feature/reminders`. The date field no longer shows the red error on open. Messages follow the order error, past time, done task, then permission info. A disabled Save press moves focus to the date field. Added `test/reminder-editor.test.js`. `npm test` passes all 110 tests. Tokens: 59,224 uncached input, 787,968 cached input, 6,908 output. The no-red-border rule was checked only in the CSS, because Chrome could not start in the sandbox.
- Lesson: Codex finished at 10:20, but the commit and push waited until 11:04 because I missed the completion wake. After launching a run, check its status file when the next turn starts.
