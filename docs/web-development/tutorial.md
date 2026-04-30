# Web Development — Tutorial

Five levels, each one a deployed project. Don't skip levels; each introduces a constraint the next assumes you've internalized. The point is **shipped sites**, not pristine ones — every level ends with a public URL.

!!! tip "Working rule"
    A deployed Level 2 site teaches more than a half-built Level 4 monstrosity. If you're stuck, simplify, deploy, and *then* iterate.

---

## Level 1 — A personal site

**Goal:** end-to-end pipeline (write → preview → deploy → real URL) on the simplest possible site.

**Project:** a single-page personal/about site. Your name, a short bio, links to whatever (GitHub, email, projects). One page, no framework, no build step.

**What you'll learn:**

- Writing semantic HTML (`<header>`, `<main>`, `<nav>`, `<article>`, `<footer>` — not just `<div>` everywhere).
- Modern CSS: a tasteful baseline (`system-ui` font, sensible line-height, max-width on body), then a 30-line stylesheet. No framework.
- A minimal JS: a theme toggle (dark/light) using `prefers-color-scheme` and a `localStorage` override.
- Deploying to Cloudflare Pages or Vercel.
- Buying a real domain (~$10/year on Cloudflare Registrar) and pointing it at the site.

**Stop conditions:** the site is at a real URL, looks decent on phone and desktop, and the dark/light toggle works.

---

## Level 2 — A static site with a build step

**Goal:** get used to a real toolchain (Node, npm, Vite, TypeScript) without yet adding the complexity of a framework.

**Project ideas:** a multi-page blog, a portfolio with a projects gallery, a documentation site. Use [Astro](https://astro.build) (file-based routing, MDX, zero JS by default) or pure Vite + TS + a few hand-written page templates.

**What you'll learn:**

- `npm init`, `package.json`, `node_modules`, lockfiles. What "installing a dependency" actually does.
- Vite's dev server + production build.
- TypeScript on day one. Configure `tsconfig.json` with `strict: true` and never look back.
- CSS at scale: variables, custom properties, `@import`, optionally a tiny utility framework (Tailwind v4, [Open Props](https://open-props.style)).
- Image optimization: responsive images, modern formats (AVIF/WebP), lazy loading.
- A real Lighthouse score: target 95+ for performance and accessibility.

**Stop conditions:** clean Lighthouse, deploys via `git push`, real domain, you can describe what every file in the project does.

---

## Level 3 — A reactive frontend

**Goal:** stop pretending the page is static.

**Project:** a single-page app with meaningful interactive state. Examples: a Pomodoro timer with a session log; a Markdown notes app with localStorage persistence; a fuzzy-searchable list of links you've collected; a simple drawing app with `<canvas>`.

**What you'll learn:**

- **React** (or Svelte, but pick one and stick with it). Components, props, state, effects, refs.
- The **rules of state**: derived state is not state; URL state is shareable state; localStorage state survives reloads.
- Forms: controlled vs uncontrolled inputs. When each is right.
- Client-side routing: [TanStack Router](https://tanstack.com/router), React Router, or SvelteKit.
- A component library OR custom CSS — not both, not yet.
- Async UX: loading states, error states, optimistic updates. You should be able to point at every box in the [state-location table](./usage.md#state-where-it-lives) for every piece of data on screen.

**Stop conditions:** the app is genuinely useful for *you*, not a toy. You'd link a friend to it without a "yeah, but..."

---

## Level 4 — Adding a backend

**Goal:** persistence and authentication. The point at which "web app" becomes a real product.

**Project ideas:** turn your Level 3 app into a multi-user version. Notes you can log into. A linkrot-resistant bookmark store synced across devices. A read-it-later app. A simple multiplayer game (turn-based, like tic-tac-toe over WebSocket).

**What you'll learn:**

- **A backend runtime**: Node.js + [Hono](https://hono.dev) or [Fastify](https://fastify.dev), or Bun + Hono. Avoid Express — it's still everywhere but the API is from another decade.
- **A database**: PostgreSQL. Run it locally with Docker; deploy via [Neon](https://neon.tech), [Supabase](https://supabase.com), or [Fly Postgres](https://fly.io/docs/postgres/).
- **Schema and migrations**: [Drizzle](https://orm.drizzle.team) or [Prisma](https://prisma.io). Drizzle has the lighter mental model.
- **Authentication**: don't roll your own. Use [Clerk](https://clerk.com), [Auth.js](https://authjs.dev), [Lucia](https://lucia-auth.com), or [Supabase Auth](https://supabase.com/docs/guides/auth). Sessions in HTTP-only cookies; JWTs only when there's a clear reason.
- **API design**: a few REST endpoints, or [tRPC](https://trpc.io) if your client and server share TypeScript.
- **Deploy strategy**: SPA + separate API (Vercel/Cloudflare Pages + Fly.io), or full-stack ([Next.js](https://nextjs.org), [SvelteKit](https://kit.svelte.dev), [Remix](https://remix.run)).

**Stop conditions:** two users in different browsers can each log in, see only their own data, and have it persist across reloads.

---

## Level 5 — A real product

**Goal:** something you'd be willing to charge money for, even if you don't.

**Constraints:**

- **Production observability**: log aggregation (Logtail, Axiom, Vercel logs), error tracking (Sentry), basic uptime monitoring.
- **CI/CD**: tests run on every PR; main auto-deploys.
- **Tests**: unit tests for pure logic (Vitest), at least one end-to-end test (Playwright) covering the critical flow.
- **Security pass**: HTTPS only, HTTP-only cookies, CSRF-aware mutations, content-security-policy header, rate-limiting on auth endpoints, parameterized queries (or an ORM that gives them to you).
- **Accessibility pass**: keyboard navigable, sensible focus rings, axe-clean, screen-reader spot-check.
- **Performance budget**: Lighthouse 90+ on real devices, not just localhost. Real-user monitoring (RUM) wired up.
- **Payments** (optional but instructive): Stripe Checkout. Even a $1 product teaches more than a thousand free dashboards.
- **Real users**: at least three people who are not you, and you've watched at least one of them use it.

**Project ideas:** a niche tool for a hobby community you're in. A SaaS dashboard around a public API. A coordination tool for a club or team. A "small bets" indie product.

**Stop conditions:** someone you don't know personally has used the site twice in a week.

---

## After Level 5

You're not "done" — but the marginal value of more tutorials is low. Pick a real product or job and grow into the topics it forces on you. Things to dig into when relevant:

- **Performance at scale**: Core Web Vitals, code-splitting, prefetching, ISR, edge rendering.
- **Realtime**: WebSockets, Server-Sent Events, [Liveblocks](https://liveblocks.io), [PartyKit](https://partykit.io), CRDTs ([Yjs](https://yjs.dev), [Automerge](https://automerge.org)).
- **Mobile**: PWAs first; React Native or Capacitor only when you've tried PWAs.
- **Animations**: [Motion](https://motion.dev) (formerly Framer Motion), View Transitions API.
- **Type-safe stacks**: tRPC, end-to-end types, Zod validators at boundaries.
- **AI integrations**: streaming LLM responses, function-calling UIs, embeddings + pgvector for search.

The [Learning](./learning.md) page has resources for each.
