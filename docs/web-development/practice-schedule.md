# Web Development — Practice Schedule

Web dev is **shipping-paced**. Hours don't translate to skill the way they do in instrument practice — *finished and deployed* projects do. The schedule below is built to keep you shipping.

!!! tip "Working rule"
    Deploy *something* every week, even if it's a one-line CSS change. The deploy reflex is the most valuable habit in web dev; let it lapse and projects stall for months.

## Daily (15–30 min) — pick one

- [ ] Read one MDN reference page for an API you used today.
- [ ] Read one section of [the React docs](https://react.dev/learn) or [the Web Platform docs](https://web.dev) and try the example.
- [ ] Solve one small thing in dev tools: inspect, profile, or fix something on a site you use.
- [ ] Open one site you admire and copy a section of its layout into a sandbox.
- [ ] 10 min of TypeScript reading: [Total TypeScript tips](https://www.totaltypescript.com), or one section of the [TS handbook](https://www.typescriptlang.org/docs/handbook/intro.html).

## Weekly (3–5 hours) — pick one

- [ ] Make progress on the current Tutorial level.
- [ ] Build a single-purpose tool you need (a JSON formatter, a unit converter, a date diffing thing). Deploy it.
- [ ] Recreate a UI pattern from a site you like (a sidebar, a modal, a table with sticky header). No framework. CSS-first.
- [ ] Read one chapter of a book from [Learning](./learning.md).
- [ ] Refactor an old project — TypeScript-ify it, upgrade dependencies, redeploy.

## Monthly — *ship something new*

This is the keystone. Every month, one new deployment with its own URL. Constraints:

- It does *something useful* — even if only for you.
- README explains what it is and how to run it locally.
- Lighthouse Performance and Accessibility ≥ 90.
- It's been used at least once after the first deploy.

Cost is $0 (Cloudflare/Vercel free tiers + a domain you might already own). Two weeks development time = a deadline.

## Quarterly — *retire or grow one project*

For each thing you've shipped, decide:

- **Grow it**: add the next obvious feature. Rewrite the gnarly part.
- **Retire it**: archive the repo, take it offline, write a one-paragraph post-mortem.

Don't let half-alive projects accumulate. The dashboard of forgotten Vercel deploys is the visual equivalent of a closet full of half-knit sweaters.

## Anti-pattern checklist

Don't do these:

- [ ] Spend > 1 week on a single Tutorial level. Ship something rough, iterate next round.
- [ ] Switch frameworks every two weeks. React or Svelte; pick once, stick for ~6 months.
- [ ] Read about web dev (think pieces, Twitter, HN) more than you build. The opinions are loud and almost none of them are load-bearing for you yet.
- [ ] Watch tutorials at 0.75x without typing. Passive learning = wasted hours.
- [ ] Set up a "perfect" config (ESLint, Prettier, Husky, lint-staged, GitHub Actions, Renovate) before the project has any features.

## Tracking

Keep a `projects.md` somewhere with one line per shipped thing:

```
2026-01  hello-web         personal site, dark mode toggle
2026-02  pomodoro          timer + session log, localStorage
2026-03  notes             markdown notes app, no backend yet
2026-04  notes-v2          + auth, + Postgres, Lighthouse 95
2026-05  link-vault        bookmarks app, used by 3 friends
```

The list is the metric, not the hours.
