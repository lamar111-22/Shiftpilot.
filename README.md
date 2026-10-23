# ShiftPilot

AI-powered assistant for volunteer coordinators. ShiftPilot turns rosters, schedules, and notes into a ready-to-staff event — drafting outreach and reminder messages, tracking shift coverage, and keeping every volunteer in the loop. Nothing is sent without your approval.

## What it does

- **Upload roster** — drop CSV, Excel, PDF, text, or image files; the agent reads them and builds your event for review.
- **Console** — one dashboard for event metrics, shift coverage, AI-drafted messages, and recent agent runs.
- **Members** — your volunteer roster with availability, tags, completed shifts, and signups.
- **Volunteer inbox** — a phone-style view of each volunteer's messages with confirm/decline replies.
- **Sent messages** — an outbox of every approved outreach and reminder, with status and delivery details.
- **Member view** — the signup page a volunteer sees to pick their shifts.
- **Plans** — Student, Club, and Nonprofit tiers for unlimited drafts and real email.

## Tech stack

React + Vite, Tailwind CSS, shadcn/ui, React Router. The backend (entities, functions, auth, integrations) runs on the Base44 platform.

## Project structure

```
src/
  pages/         # Console, Intake, Members, Outbox, Plans, Signup, VolunteerInbox, ThankYou
  components/    # Layout, ShiftCard, DraftCard, and shared UI primitives
  lib/           # appData.js (shared app state), auth, utils
base44/
  entities/      # Event, Shift, Member, Signup, Message, AgentRun, Settings
  functions/     # AI agent steps (fill shifts, draft reminders, intake files, …)
  workflows/     # triggered automations
```

## Run locally

Prerequisites: Node.js, the Base44 CLI (`npm install -g base44@latest`), and [Deno](https://docs.deno.com/runtime/getting_started/installation/).

```bash
npm install
base44 login   # one-time per machine
base44 link    # one-time per clone
base44 dev     # local backend + frontend together
```

Open the frontend URL `base44 dev` prints (typically `http://localhost:5173`).

Notes:

- **Every fresh clone needs `base44 link`.** It writes `base44/.app.jsonc` (the app-id pointer), which is gitignored. Find your app id in the Builder URL (`app.base44.com/apps/<id>/...`).
- **`base44 dev` runs the frontend for you** — never run `npm run dev` alongside it; a standalone Vite serves a UI with no backend behind it.
- **The app must be published at least once** for the UI to load under `base44 dev`; the frontend boots by fetching settings from the hosted app.
- Entity data is **in-memory only** and wiped when `base44 dev` restarts. Everything else (Core integrations, OAuth) forwards to your deployed app.

### Frontend only, hosted backend

```bash
base44 dev --remote
```

Writes go to your app's **production data** in this mode — plain `base44 dev` keeps everything local.

## Publish your changes

This repo syncs to Base44 through git, so publish from the dashboard:

```bash
base44 dashboard open
```

Avoid `base44 deploy` — it ships your local tree directly and the deployed state silently diverges from the repo.

## Docs & support

- GitHub integration: https://docs.base44.com/developers/app-code/local-development/github
- Local development: https://docs.base44.com/developers/backend/overview/local-dev/local-development-overview
- Support: https://app.base44.com/support