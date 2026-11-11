# KeyRush — Typing Speed Test

A polished, responsive typing speed test web app. Race the clock, track your WPM and accuracy, earn points and badges, and climb the leaderboard.

Built with **React**, **TypeScript**, **Vite**, **Tailwind CSS**, and **Supabase** (auth + database).

## Features

### Typing game
- Test durations of **15, 30, 60, and 120 seconds**
- Four practice modes: **words**, **quotes**, **code**, and **custom text**
- Character-by-character feedback (correct / incorrect / current position)
- Live countdown, WPM, accuracy, and correct/incorrect character counts
- Pause, resume, restart, and new-passage controls
- Results screen with final stats, points earned, and badges unlocked
- Timer starts on the first keystroke; fully playable on mobile

### Game progression
- Points for every completed test, scaled by speed and accuracy (bonus above 90%)
- Seven level tiers with a progress bar
- Badges for milestones (speed thresholds, flawless runs, test counts)
- Progress panel with personal best, average WPM, accuracy trend, tests completed, and recent results

### Accounts & leaderboard
- Guests can play everything — no sign-up required
- Optional email/password accounts (Supabase Auth) save results automatically
- Leaderboard with **weekly** and **all-time** views, ranked by points
- Clearly labeled sample rankings appear when there aren't enough real player scores yet

## Getting started

```bash
npm install
npm run dev
```

The dev server runs automatically in Bolt. For local development outside Bolt, create a `.env` file with your Supabase project credentials:

```
VITE_SUPABASE_URL=<your-project-url>
VITE_SUPABASE_ANON_KEY=<your-anon-key>
```

## Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the dev server |
| `npm run build` | Production build |
| `npm run preview` | Preview the production build |
| `npm run typecheck` | TypeScript type-check |
| `npm run lint` | ESLint |

## Database

The schema lives in `supabase/migrations/` and is applied through the Supabase MCP tools:

- **`profiles`** — display names, created automatically on sign-up via a trigger
- **`test_results`** — one row per completed test (WPM, accuracy, characters, duration, mode, points)
- **`demo_leaderboard`** — seeded sample rows shown when real player data is sparse

Row Level Security is enabled on every table: results are writable only by their owner, profiles are read-only to others, and the demo table is read-only.

## Project structure

```
src/
├── App.tsx                  # Layout, nav, footer, auth state, toasts
├── components/
│   ├── TypeTest.tsx         # The typing game and results screen
│   ├── Leaderboard.tsx      # Weekly / all-time rankings
│   ├── Progress.tsx         # Levels, badges, stats, recent results
│   ├── AuthModal.tsx        # Sign-up / login dialog
│   └── Sections.tsx         # Hero, highlights, how-it-works, FAQ
└── lib/
    ├── supabase.ts          # Supabase client
    ├── backend.ts           # Auth, results, and leaderboard queries
    ├── scoring.ts           # Points, levels, badges, stats helpers
    └── content.ts           # Word lists, quotes, code snippets, passage generator
```
