# Web Development — Best Practices

Conventions, security/perf/a11y habits, and production reflexes. Roughly ordered "applies to Level 1" → "applies once you have real users."

## HTML

- **Semantic tags first.** `<header>`, `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>`, `<footer>`, `<button>`. Reach for `<div>` / `<span>` only when no semantic option fits.
- **Buttons and links are different.** A `<button>` does an action; an `<a href>` navigates. Never use a `<div onclick>` for either — you'll lose keyboard access, focus rings, and screen-reader semantics.
- **Always include `<meta name="viewport">`.** Mobile breaks without it.
- **Always set `<html lang>`.** Affects screen readers, hyphenation, browser translation prompts.
- **Forms have `<label for>` connected to inputs.** Or wrap the input in the label. Either works; *no* label is wrong.
- **Use the right input types.** `email`, `tel`, `url`, `number`, `date`. Mobile keyboards adapt automatically.

## CSS

- **Mobile-first, not desktop-first.** Default styles target small screens; `@media (min-width: …)` adds desktop layout.
- **Use logical properties.** `margin-block-start`, `padding-inline`, `inset` — not `margin-top`, etc. Future-proof for RTL languages.
- **`rem` and `em` over `px`** for anything user-scalable (text, spacing). `px` is fine for hairline borders.
- **Set up CSS custom properties for design tokens** early — `--color-fg`, `--space-2`, `--radius-md`. A 30-line token file is enough.
- **Container queries** (`@container`) are usable in 2025. Reach for them when a component should respond to *its container's* width, not the viewport's.
- **`prefers-reduced-motion`** — wrap any non-essential animation in `@media (prefers-reduced-motion: no-preference)`.
- **Don't fight the cascade.** Specificity wars usually mean the architecture is wrong. Use `:where()` to keep selectors specificity-zero, or move to a utility framework.

## JavaScript / TypeScript

- **TypeScript with `strict: true`** from day one. The migration tax later is brutal.
- **`unknown` over `any`.** `any` turns off type checking; `unknown` forces you to narrow before using.
- **Validate at boundaries.** Anything from `fetch`, `JSON.parse`, `localStorage`, URL params, or user input is `unknown`. Validate with [Zod](https://zod.dev) or [Valibot](https://valibot.dev) before letting it into typed code.
- **Avoid classes in modern JS unless you have a reason.** Functions and plain objects compose better.
- **`async`/`await`** over raw `.then()`. Easier stack traces, easier control flow.
- **Don't catch errors you can't handle.** Let them bubble to a top-level handler that logs to Sentry. Catching to silently `console.error` is worse than not catching.
- **AbortController for cancellable fetches.** Especially in components that can unmount mid-request.

## React (when you use it)

- **Lift state only as far as it needs to go.** A modal's open/closed state belongs near the modal, not in a global store.
- **Derived state is not state.** If `fullName = first + ' ' + last`, just compute it; don't `useState`+`useEffect` it.
- **`useEffect` is for syncing with external systems** (subscriptions, timers, the DOM). It's *not* for "run code when this prop changes."
- **Keys** must be stable IDs from your data, never array indexes for lists you can reorder.
- **Server state ≠ client state.** Use [TanStack Query](https://tanstack.com/query) (or your framework's loader) for anything fetched. Don't reinvent caching with `useState`.
- **Don't optimize before measuring.** `useMemo`/`useCallback` sprinkled everywhere usually slows the app. Profile first.

## Accessibility (a11y)

- **Keyboard-only pass** every time you ship. Tab through every interactive element. If you can't reach it or use it, it's broken.
- **Visible focus rings.** Don't blanket-`outline: none`. If you don't like the default, replace it; don't remove it.
- **Color contrast ≥ 4.5:1** for body text. Use the dev tools color picker to check.
- **Alt text on images.** Decorative images get `alt=""`, not no alt at all.
- **Form errors associated with inputs.** `aria-describedby` pointing at the error message; `aria-invalid="true"` on the input.
- **Use [axe DevTools](https://www.deque.com/axe/devtools/)** as a baseline. It catches the easy stuff. Manual testing catches the rest.

## Performance

- **Set a budget**: target Lighthouse 90+ on mid-tier mobile, on a throttled connection, before launch.
- **Images are the #1 win.** Modern format (AVIF/WebP), `loading="lazy"`, correct `sizes`/`srcset`, dimensions in HTML to prevent layout shift.
- **Fonts**: use `font-display: swap`. Self-host critical fonts or use a font CDN that supports it.
- **JS bundle size**: split routes, lazy-load anything below the fold. Audit dependencies — moment.js (use date-fns/Temporal), lodash (use individual imports or vanilla), big icon libraries (tree-shake).
- **Cache headers**: long `max-age` + immutable for hashed assets; short for HTML.
- **Avoid layout thrashing**: read all DOM measurements before any writes within a frame.
- **Real user monitoring** > synthetic. Lighthouse on your laptop is not your users' experience.

## Security

These are the floor. Don't skip any.

- **HTTPS everywhere**, including local-dev where feasible (Vercel/CF give you HTTPS dev URLs).
- **HTTP-only, Secure, SameSite=Lax cookies** for sessions. JWTs in localStorage = XSS = stolen tokens.
- **Parameterized queries.** ORMs/SQL builders give them to you; raw string concatenation does not.
- **Validate every input on the server.** Client-side validation is a UX feature, not a security feature.
- **CSRF protection** on state-changing endpoints (mutations). Same-site cookies cover most cases; double-submit token cookies cover the rest.
- **Rate-limit auth endpoints** (login, signup, password reset). Cloudflare can do this for free.
- **Content-Security-Policy** header — start permissive, tighten over time.
- **Dependencies**: enable Dependabot or Renovate. Run `npm audit` periodically.
- **Secrets**: never in client bundles. Even "anon" keys for services like Supabase need RLS rules to be safe.

## Git / repo hygiene

- **Conventional commits** are nice but not required. *Descriptive* commit messages are required.
- **`.gitignore` from day one**: `node_modules/`, `.env`, `.env.local`, build artifacts, OS files (`.DS_Store`).
- **`.env.example`** committed; `.env.local` in gitignore. Never commit real secrets, ever.
- **Small PRs.** Review-able PRs are < ~400 lines diff. Anything bigger should be split.
- **Tag deployed releases**: `git tag v1.0.0` per real launch.

## Deployment / production

- **Preview deploys per branch.** Vercel and Cloudflare Pages do this automatically; use them.
- **Health-check endpoint** (`/healthz`) returning 200 + a tiny JSON payload. Uptime monitors hit it.
- **Structured logging**: JSON, not `console.log("user did " + thing)`. Logtail/Axiom can index it.
- **One environment per env**: `dev`, `staging`, `prod`. Same image, different config.
- **Migrations run before code deploys**, not from the app itself on first request. Drizzle Kit, Prisma Migrate, etc. — wire them into CI.
- **Rollback plan**: know how to revert the previous deploy. Most platforms give one-click rollback.

## Habits worth forming

- **Open dev tools every session.** Network panel, Console, Elements. The site you're building *and* sites you visit.
- **Read MDN before npm.** New API? MDN first. There's almost certainly a built-in.
- **Ship Friday afternoon, monitor Saturday morning.** Just kidding — don't deploy on Fridays unless rollback is one click and tested.
- **Keep a `learnings.md`** in each project. One line per "I lost an hour to this."
- **Open one of your old projects every month.** Half of all design wisdom is "the thing past me did wrong."
