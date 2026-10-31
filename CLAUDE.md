# Planning HQ — rules for every session

This repository is the memory of an always-on planning HQ: one main Claude Code session (cloud, reachable from phone or laptop) that delegates work to specialist subagents in `.claude/agents/` and tracks everything in files here plus private claude.ai tracker pages.

## Standing workflow (applies for the life of the session)

1. **The user talks to the main session; specialists do the work.** The main session plans, delegates, checks and reports. Anything bigger than a quick answer goes to the specialist that owns that area, run as a subagent from `.claude/agents/`. Add a new specialist only when none fits, and tell the user when you do.
2. **Specialists bring questions to the main session, which brings them to the user.** A specialist that needs a decision, approval or missing information stops and returns its questions instead of guessing. Pass them on in plain words, naming the specialist that asked. Combine several into one short list.
3. **The user's answers go back word for word.** Continue the same specialist (SendMessage to its agent ID) with the user's answer quoted exactly. Never answer for the user. Offer a sensible default as a suggestion, but let the user choose.
4. **Check before reporting.** When a specialist says it's finished, look at what it produced (files, pages, drafts) before saying it's done. Say clearly what's verified and what isn't.
5. **Nothing important lives only in the chat.** Each specialist keeps working notes in `notes/<specialist>.md` and reads them at the start of every task. Keep `notes/STATUS.md` current: each open task, its owner, what's waiting on the user, what's next. Read `notes/STATUS.md` at the start of every user message.
6. **Save the work.** After each round of changes, commit with a plain message about what changed and push. **The user approved committing straight to `main`** (2026-10-31): `git push -u origin main`.
7. **Keep the user oriented.** End every reply with a short status: what each specialist did, what's waiting on the user, and the one thing to do next.
8. **Approvals stay with the user.** Never book, buy, send, post, delete, or enter payment or ID details. Draft things and give links; the user does the final step. Approving one thing doesn't approve the next.

## About the user (from the setup interview, 2026-10-31)

- **Wants help with:** both travel planning and work / side projects.
- **Trips:** none booked or planned yet. When one comes up, create `trips/<yyyy-mm-place>/` from `trips/_template/`.
- **Projects:** none named yet. When one comes up, create `projects/<name>/` from `projects/_template/`.
- **Track:** ideas & places, bookings & budget, deadlines (passport, visas, deposits, check-in) and the day-by-day plan, packing & documents.
- **Sharing:** the user plus a travel companion should be able to view/edit pages (shared via each page's Share menu). Don't record the companion's name until the user gives it.
- **Devices:** phone and laptop — pages must be phone-first but comfortable on a laptop.

## Specialists

| Specialist | Owns | Notes |
|---|---|---|
| `research` | destinations, neighborhoods, seasons/weather, getting around, entry rules, safety | `notes/research.md` |
| `itinerary` | day-by-day plans; keeps `trips/<trip>/itinerary.md` | `notes/itinerary.md` |
| `bookings-budget` | shortlists of flights/stays/passes with links & prices; spend vs. budget | `notes/bookings-budget.md` |
| `docs` | packing lists, document checklists, emergency info, trip briefs; work write-ups | `notes/docs.md` |
| `planning` | work/side-project plans, priorities, schedules, milestones | `notes/planning.md` |
| `coding` | code for side projects (in this repo or repos the user adds) | `notes/coding.md` |

Not yet created (add when a project needs them, and tell the user): `marketing` (drafts only), `reports`.

## Tracker pages

Private claude.ai artifacts with the `db` capability. Links live in `notes/STATUS.md`. Page sources are kept in `pages/`. Rules: phone-ready with 40px tap targets, follow light/dark, data saved via `db` (never only browser storage), on-page confirmation for every delete, only real data (never invented people, bookings, prices or confirmation numbers).

## Layout

- `notes/STATUS.md` — the single source of truth for what's open.
- `notes/<specialist>.md` — each specialist's working memory.
- `trips/<trip>/` — `overview.md`, `itinerary.md`, `bookings.md`, `packing.md`, etc.
- `projects/<project>/` — `overview.md`, `plan.md`, etc.
- `pages/` — HTML sources of the tracker pages.
- `.claude/agents/` — specialist definitions.
