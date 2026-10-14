# GitLook

Look up any GitHub user and see their profile, contribution streaks, heatmap, languages, top repos and recent activity — in one dashboard.

Frontend only (React). No backend, no database: everything is fetched straight from the browser.

## Features

- **Profile** — avatar, bio, company, location, links, account age, follower ratio
- **Stats** — repos, stars earned, forks, followers, contributions (12 months & all-time)
- **Streaks** — current streak, longest streak (all-time, with dates), best day, busiest weekday
- **Contribution heatmap** — GitHub-style calendar for the last 12 months or any year
- **Charts** — contributions per month / weekday / year, top languages, most-starred repos, activity by hour of day, event-type breakdown
- **Repositories** — searchable, filterable (language, hide forks), sortable grid
- **Recent activity** — pushes, PRs, issues, stars, releases (last 90 days)
- **Insights** — night owl vs early bird, favourite language, hot repo, etc.
- **Compare** — `/compare/userA/userB` side by side
- Recent searches, shareable URLs (`/u/<username>`), dark/light mode, loading skeletons, friendly errors

## Tech

Vite · React 19 · React Router 7 · Tailwind CSS 4 · Recharts

## Run it

```bash
npm install
npm run dev        # http://localhost:5173
npm run build      # production build in dist/
npm run preview    # serve the build
```

## Data sources

| Data | Source |
|---|---|
| Profile, repos, events, orgs, followers | GitHub REST API (`api.github.com`) |
| Contribution calendar (streaks, heatmap) | [github-contributions-api](https://github-contributions-api.jogruber.de) — or GitHub GraphQL when a token is set |

### Rate limits

Without a token, GitHub allows **60 requests/hour** per IP (one profile ≈ 4–7 requests). Responses are cached in `sessionStorage` for 10 minutes. The header shows how many requests are left.

To raise the limit to 5,000/hour, click the ⚙️ icon and paste a GitHub personal access token (no permissions/scopes needed — public data only). The token is stored only in your browser's `localStorage`.

## Project structure

```
src/
├── api/          # github.js (REST + GraphQL), contributions.js, storage.js (cache)
├── hooks/        # useGithubUser — loads all data for a username
├── utils/        # stats.js (streaks, summaries), format.js, languageColors.js, recent.js
├── components/   # ProfileCard, StreakCard, ContributionHeatmap, Charts, RepoList, ...
└── pages/        # Home, Profile, Compare, NotFound
```

## Deploy

It's a static site — deploy `dist/` anywhere (Vercel, Netlify, GitHub Pages). For client-side routes, configure a SPA fallback to `index.html` (Vercel/Netlify do this automatically for Vite with a rewrite rule).
