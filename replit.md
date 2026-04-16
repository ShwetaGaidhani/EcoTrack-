# EcoTrack Workspace

## Overview

EcoTrack is an eco-friendly lifestyle web app that helps users adopt sustainable habits, track their carbon footprint, and earn rewards. Built as a full-stack pnpm monorepo with a React + Vite frontend and Express API backend.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite + Tailwind CSS (Material-inspired, light eco-green palette)
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Charts**: Recharts
- **Animations**: Framer Motion

## Key Features

- **Dashboard**: Carbon saved, points, streaks, weekly trend chart, recent completions
- **Habit Tracker**: 4 categories (Energy, Transport, Food, Waste), mark-as-done with optimistic UI
- **Carbon Footprint Tracker**: Log distance, electricity, waste → auto-calculated CO2, weekly/monthly charts
- **Rewards**: Points system, badge progression (Beginner → Eco Warrior → Eco Hero → Green Master → Planet Guardian), leaderboard
- **Community Challenges**: Join eco challenges (No Plastic Week, Meat-Free Month, etc.)
- **Profile**: User stats overview

## Architecture

```
artifacts/ecotrack/     # React + Vite frontend
artifacts/api-server/   # Express 5 API backend
lib/api-spec/           # OpenAPI spec + Orval codegen config
lib/api-client-react/   # Generated React Query hooks
lib/api-zod/            # Generated Zod validation schemas
lib/db/                 # Drizzle ORM + PostgreSQL schema
```

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

## API Routes

- `GET /api/dashboard` — full dashboard summary
- `GET/POST /api/habits` — list/create habits
- `POST /api/habits/:id/complete` — mark habit done
- `GET /api/habits/completions` — completion history
- `GET/POST /api/carbon` — list/create carbon entries
- `GET /api/carbon/trends` — weekly/monthly CO2 charts
- `GET /api/rewards` — points, badges, progress
- `GET /api/rewards/leaderboard` — leaderboard
- `GET /api/community/challenges` — challenges list
- `POST /api/community/challenges/:id/join` — join challenge

## Database Tables

- `habits` — eco habit definitions
- `habit_completions` — completion history (used for points)
- `carbon_entries` — daily CO2 footprint logs
- `challenges` — community challenges

## Carbon Calculation

CO2 (kg) = (distance_km × 0.21) + (electricity_kwh × 0.233) + (waste_kg × 0.1)

## Badges

| Badge | Points Required |
|-------|----------------|
| Beginner | 0 |
| Eco Warrior | 100 |
| Eco Hero | 300 |
| Green Master | 600 |
| Planet Guardian | 1000 |
