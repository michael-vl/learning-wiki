# Web Development — Examples

Concrete project ideas, mapped to Tutorial levels. Pick one per level and deploy it. Avoid the trap of designing a "Twitter clone" before you can finish a personal site.

## Level 1 — One static page

- **Personal site / about page** — name, bio, links. The default starting point.
- **Single-purpose joke site** — `is-it-friday.com`, `should-i-deploy-on-friday.com`. Trivial CSS, memorable.
- **Wedding / event landing page** — date, venue, RSVP link. Real constraint, real audience.
- **Linktree clone** — flat list of buttons; one HTML file.

Constraints: one HTML file, < 100 lines of CSS, < 30 lines of JS, no build step.

## Level 2 — Static site with a build

- **Blog** with Astro + MDX. RSS feed. Three posts minimum.
- **Documentation site** for a tiny side project (yours or a friend's).
- **Photo gallery** with responsive `<img srcset>`, AVIF/WebP, lazy-loading. Lighthouse 95+.
- **Recipe collection** — your own recipes; full-text search over them at build time.
- **Resume / CV site** — printable, uses CSS `@media print` correctly.

Constraints: Astro/Vite + TypeScript, Lighthouse ≥ 95, deployed via `git push`.

## Level 3 — Reactive frontend (no backend yet)

- **Pomodoro timer** with a session log in localStorage.
- **Markdown notes app** — split-view editor, localStorage save, export to file.
- **Drum machine / step sequencer** with WebAudio.
- **Habit tracker** — a calendar grid, click to mark days.
- **Calculator** with full keyboard support and an undo stack.
- **Chess clock**, **stopwatch with laps**, **word counter** — small, focused.
- **Hash / encoding tool** — base64, URL-encoding, JSON pretty-print, JWT inspector.

Constraints: React or Svelte; URL state for anything shareable; localStorage for preferences; keyboard navigable.

## Level 4 — Full-stack (frontend + backend + DB)

- **Multi-user notes app** — Level 3 notes app + auth + Postgres.
- **Bookmark manager** — per-user bookmarks, tags, full-text search via Postgres `tsvector`.
- **Read-it-later** — paste a URL, server fetches and stores readable HTML, you can read later.
- **Habit tracker, multi-user** — share a habit with a friend; see each other's streaks.
- **Tiny Trello clone** — boards, lists, cards. Drag-and-drop. Single user is fine.
- **Pet sitter scheduling app** — for a hobby community you're already in.
- **Self-hosted RSS reader** — feed list, item view, marked-as-read state.

Constraints: real auth, real database, two browsers can each log in and see only their own data.

## Level 5 — Production-y product

- **Niche SaaS** — a tool for *one* hobby/community you're part of. Charge $5/mo, even just to one friend.
- **Open-source dashboard for a public API** — pulls from a public dataset (city open data, GitHub stats), updates daily, has an audience.
- **A "small bets" tool** — see [@levelsio](https://twitter.com/levelsio) for the genre. One-purpose, well-marketed, profitable.
- **Internal tool for your day job** — solves a real problem, has real users (your coworkers).

Constraints: tests run on CI, errors go to Sentry, real users use it, basic security pass clean.

## Reference sites worth reading

Open dev tools and inspect; copy techniques you see.

- **[every-layout.dev](https://every-layout.dev)** — the canonical CSS-pattern reference.
- **[joshwcomeau.com](https://www.joshwcomeau.com)** — a site that *is* the lesson. Read source.
- **[paulstamatiou.com](https://paulstamatiou.com)** — a long-running personal site, beautifully crafted.
- **[bartoszcielonka.dev](https://www.bart.dev)** and other personal sites you find on Hacker News' "Who Is Hiring" — typography lessons.
- **[Stripe.com](https://stripe.com)** — the industry reference for marketing-page craft.
- **[Linear.app](https://linear.app)** — likewise for app UI.

## Open-source projects worth reading code from

- **[Cal.com](https://github.com/calcom/cal.com)** — full-stack Next.js, big enough to be realistic, small enough to navigate.
- **[Bluesky web app](https://github.com/bluesky-social/social-app)** — React Native + web, real product complexity.
- **[Excalidraw](https://github.com/excalidraw/excalidraw)** — SPA, canvas-heavy, well-tested.
- **[Plausible](https://github.com/plausible/analytics)** — Phoenix/Elixir backend with a clean web frontend; useful contrast to JS-everywhere.
- **[VSCode source](https://github.com/microsoft/vscode)** — read selectively, but a masterclass in TS-at-scale.

Reading other people's deployed code is the fastest route past the framework-tutorial plateau.
