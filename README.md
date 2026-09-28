# Kolkata Metro Timeline API

Explore the Kolkata Metro network, look up station and train schedules, and plan journeys through an interactive web app backed by a REST API.

> **Travel note:** Schedule information is indicative. Confirm service details with Metro Railway Kolkata before travelling.

## On this page

- [What you can do](#what-you-can-do)
- [Explore the app](#explore-the-app)
- [Quick start](#quick-start)
- [Environment variables](#environment-variables)
- [API at a glance](#api-at-a-glance)
- [Available commands](#available-commands)
- [Tech stack](#tech-stack)

## What you can do

- Browse a map of metro lines, stations, and interchanges.
- View line details, station information, and timetables.
- Check station timelines and upcoming departures.
- Plan a journey between stations.
- Review date-specific schedule exceptions, such as holiday or festival services.
- Try API requests and inspect JSON responses in the built-in API console.

## Explore the app

| Section | What you'll find |
| --- | --- |
| **Network** | Interactive network map, lines, stations, and interchanges |
| **Timetable** | Service times and frequency bands |
| **Journey** | Route planning between stations |
| **Exceptions** | Date-specific schedule changes |
| **API Console** | Browse the API catalogue, run requests, and inspect JSON |

## Quick start

### Requirements

- Node.js **20.19+** or **22.12+**
- npm
- A Supabase project for the API data
- Vercel CLI for running the API locally

### Install and run

```bash
npm ci
npx vercel dev
```

Vercel CLI serves the Vite app and the `/api` serverless functions together. Configure the environment variables below before making requests that need the database.

To run only the frontend with Vite:

```bash
npm run dev
```

The frontend expects the API at `/api`; use `npx vercel dev` when you want the API functions available locally as well.

### Build and preview

```bash
npm run build
npm run preview
```

## Environment variables

Keep credentials out of source control. For local development, create an untracked `.env.local` file in the project root; for deployment, set variables in your hosting provider's environment settings.

| Variable | Required | Purpose |
| --- | --- | --- |
| `NEXT_PUBLIC_SUPABASE_URL` | Yes, for database-backed API routes | Supabase project URL used by the server-side API |
| `SUPABASE_SERVICE_ROLE_KEY` | Yes, for database-backed API routes | Server-side Supabase credential. **Never expose it in client-side code or commit it.** |
| `FULLSTACK_PROJECT_REF` | No | Project reference used by the optional database restore hook |
| `FULLSTACK_RESTORE_API_URL` | No | Restore endpoint used by the optional database restore hook |

The service-role key is privileged. Store it as a server-side secret in Vercel; do not add it to a `VITE_` variable or publish it in configuration files.

## API at a glance

The REST API is served under `/api`. Successful responses use JSON; schedule times use the `HH:MM` 24-hour format, including `24:xx` for after-midnight service.

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/api/lines` | List metro lines |
| `GET` | `/api/lines/{lineId}/schedule` | Get a line schedule |
| `GET` | `/api/stations` | List and filter stations |
| `GET` | `/api/stations/{stationId}/timeline` | Get station arrivals and departures |
| `GET` | `/api/interchanges` | List interchange stations |
| `GET` | `/api/route?from={stationId}&to={stationId}` | Plan a journey |
| `GET` | `/api/exceptions` | List schedule exceptions |
| `POST` | `/api/exceptions` | Create a schedule exception |

The API console provides the full, self-describing endpoint catalogue, including parameters and request examples.

<details>
<summary>Try a few requests</summary>

```bash
# List metro lines
curl http://localhost:3000/api/lines

# Get the station timeline
curl http://localhost:3000/api/stations/esplanade/timeline

# Plan a journey
curl "http://localhost:3000/api/route?from=dakshineswar&to=salt-lake-sector-v"
```

When using a different local port or a deployed app, replace `http://localhost:3000` with that app's origin.

</details>

## Available commands

| Command | Description |
| --- | --- |
| `npm ci` | Install the exact dependency versions in the lockfile |
| `npm run dev` | Start the Vite frontend development server |
| `npx vercel dev` | Run the app with Vercel serverless API routes locally |
| `npm run build` | Type-check and create a production frontend build |
| `npm run preview` | Preview the production frontend build |
| `npm run lint` | Run ESLint |

## Tech stack

- React and TypeScript
- Vite
- Tailwind CSS
- React Router
- Vercel serverless API routes
- Supabase

