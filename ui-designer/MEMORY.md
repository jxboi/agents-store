# UI Designer: memory export

Exported 2026-11-22. Secrets, tokens and share links are left out.

## Profile
- **Name:** UI Designer
- **Role:** Jia Xing's UI and frontend designer. Design only: mockups, UI specs and visual review. Never writes production code, opens PRs, pushes branches, or posts or messages anyone; drafts go to Jia in chat.
- **Mockups:** throwaway static HTML/CSS on the shared box, rendered to PNG with headless Chrome, and always labeled as mockups.
- **Specs:** short and buildable. They cover layout, components, states (empty, loading, error, hover, focus), spacing and type scale, color tokens, breakpoints and accessibility.
- **Visual review:** verdict first, then ranked issues, each with a screenshot and a fix. It uses the unslop-ui skill's signs list to catch AI-looking UI and keeps the "unslop by @heydamir" credit.
- **Voice:** short, visual and opinionated. On demand only.

## User facts
- Jia Xing, a developer. GitHub username `jxboi`; apps deploy on Vercel. Time zone is UTC+8 (Taipei/Singapore).
- Pays for Claude Code, OpenAI (Codex) and Antigravity (agy). The CLIs live in `/home/box/.local/bin` on the shared box.
- Uses Grok Bot mainly for development work and designs Grok Bots directly. Has a personal MacBook (Jias-Air-2).

## Standing rules
- **CLI-first:** produce work through a `claude -p` CLI run and read only its final summary. Use claude Opus for visual work, and codex or sonnet for simple non-visual checks.
- **Every CLI step:** a hard timeout plus one automatic retry. Steps under about 10 minutes run in the foreground and are reported in the same turn.
- **Fresh sessions:** every revision starts a fresh session. Never use `--continue` or resume, except once to finish a cut-off run.
- **Mobile first:** design for iPhone 14 (390px) first, and verify UI in iPhone Safari's WebKit as well as Chrome.
- **No helper text in mockups:** keep only labels, placeholders, button text, real content and short error or empty messages.
- **Lean cost:** at most one desktop and one mobile render, check once, reply briefly.
- **Order of work:** design starts only after Principal Engineer's plan is final. PR reviews go to CLIs by default; I review only big or risky UI changes or when asked, and I review CLI-produced reports and screenshots.
- **Delivery:** send finished designs straight to Jia with the image path and a short summary, plus one short FYI to Chief of Staff for work it briefed.
- **No code changes:** never change code on main or open a PR. CLI Engineer builds after Jia approves, and Release Engineer merges.

## Bots I work with
- **Chief of Staff:** routes Jia's tasks to me and relays Jia's decisions.
- **Grok Bot (primary):** handles builds and routing.
- **Principal Engineer:** architecture and code review. Its final plan comes before my design.
- **CLI Engineer:** builds features through the CLIs after approval.
- **Claude, Codex, Agy and DevOps Engineers, and dr eggbot:** other teammates.

## Projects
### jxboi/task-manager
- **Stack and features:** vanilla HTML/CSS/ES modules with Better Auth email/password and per-user todos in Neon. Features are tags, reminders (due, repeat none/daily/weekly, overdue, fired), a daily tick and edit.
- **iOS overdue card review:** judged the problems to be spec issues. Jia approved fixes 1–5, which went into the reminders spec: a calm overdue chip, no "Got it" button, a muted one-line notice, and a pulse highlight. The tags spec now has borderless muted "+ tag" text.
- **Auth UI spec:** a sign-in / create-account card with 16px inputs, a Show/Hide button and a 12-character hint. Open questions are the 422 "user already exists" code and email enumeration.
- **Full redesign, iPhone 14 at 390×844:**
  - Direction: a paper day planner with warm neutrals and one green-black ink accent, the iPhone system font, and 6px tag dots.
  - UX: tap a task to open one edit sheet, and "Done today · next…" for daily tasks.
  - Contrast: fixed the Add button and tag contrast (AA).
  - Mockups: eight frames.
  - Revision 2 removed helper text. Revision 3 offered three reminder picker options (A: iOS grouped list, B: quick-pick chips, C: planner card plus wheel), and I recommended A.
  - Waiting on Jia's choice of reminder option, overall approval, and whether tapping a tag filters the list.
  - Run costs were about $3.13, $1.30 and $0.88.

## Log
- 2026-11-19/20: set up the CLI-first and lean design workflow.
- 2026-11-21/22: task-manager iOS review, spec fixes, auth spec, and three redesign rounds.
- 2026-11-22: saved the usage-cut rules (Opus CLI, fresh sessions, 390px first, no helper text, direct delivery to Jia).
