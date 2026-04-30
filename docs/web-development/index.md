# Web Development — Beginner to Advanced

!!! tip "If you only do one thing"
    Build and deploy something tiny *this week*. A single HTML page on Cloudflare Pages or Vercel beats a half-finished React tutorial. Web development is a discipline of *shipping*; nothing else trains the right reflexes.

!!! warning "Don't start with a framework"
    React/Next/Svelte before HTML, CSS, and the DOM is the most common dead end. The frameworks are *abstractions over the platform*. Without the platform underneath, every error message is magic. Read [Usage](./usage.md) "The platform" before any framework tutorial.

A guide to modern full-stack web development — the browser platform, the request/response cycle, TypeScript, a component framework, a backend, a database, and deployment. Opinionated where the cost of optionality is highest (TypeScript: yes; framework: React first); pluralist where it doesn't matter (CSS framework, hosting provider).

## Scope

- **The platform** — HTML, CSS, JavaScript, the DOM, fetch, browser dev tools.
- **TypeScript** — types as documentation, structural typing, the `unknown` / `any` distinction.
- **Frontend frameworks** — React first (most jobs, biggest ecosystem); Svelte or Solid as alternatives once you understand React's model.
- **Backend** — Node.js / Bun, HTTP servers, REST and a touch of RPC, auth basics.
- **Databases** — SQL (Postgres) before NoSQL. Schema design, migrations, indexes.
- **Deployment** — static hosting, edge functions, containers. Domains, TLS, observability.
- **The async/concurrency model** — promises, event loop, cancellation. The thing that bites everyone twice.

## Sections

1. [Quickstart](./quickstart.md) — ship one HTML page in 30 minutes
2. [Usage](./usage.md) — the platform, the toolchain, mental models
3. [Tutorial](./tutorial.md) — Level 1 (static page) → Level 5 (full-stack product)
4. [Practice Schedule](./practice-schedule.md) — daily/weekly cadence
5. [Examples](./examples.md) — concrete projects at each level
6. [Best Practices](./best-practices.md) — conventions, security, performance, accessibility
7. [Learning](./learning.md) — curated resources

## The single most important mental model

The web is **a network of documents loaded by a stateless client**, layered upon by:

1. **Style** (CSS) — *declarative* rules over a tree of elements.
2. **Behavior** (JavaScript) — *imperative* code that mutates that tree, listens to events, and talks to the network.
3. **State** (frameworks/databases) — the layer humans add on top because steps 1 and 2 alone don't compose.

Frontend frameworks (React, Svelte, etc.) exist to manage step 3 *while still ultimately producing a DOM*. Servers and databases exist because the client is stateless and untrusted.

Almost every confusing web bug is a confusion about *where state lives* — in the URL, in the DOM, in a JS variable, in a cookie, in localStorage, in a server session, in a database row, in a CDN cache. Learning to name the boxes is half the skill.

## Two important corollaries

- **The browser is your IDE.** Chrome/Firefox dev tools are not a debugger you reach for occasionally; they're the primary inspection tool. Open them every session.
- **The network panel never lies.** When the UI says one thing and the data says another, the network panel resolves it. Get fluent with it before any framework.
