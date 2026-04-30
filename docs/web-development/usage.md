# Web Development — Usage

The orientation guide. Read this *before* the Tutorial. Web dev has no single editor — it's a stack of platforms (browser, runtime, network, server) plus a moving toolchain. Naming the layers is the first skill.

## The platform

Three primitives, layered:

| Layer | Language | What it does |
|---|---|---|
| Structure | **HTML** | Tree of elements (the DOM). |
| Style | **CSS** | Declarative visual rules over the tree. |
| Behavior | **JavaScript** | Imperative code that listens to events and mutates the tree. |

Everything else — frameworks, build tools, design systems — sits on top of these three. None of it replaces them.

### The DOM

The DOM is **a tree of objects**, not a string of text. The HTML you write is *parsed* into the DOM at load. From then on, the DOM is the source of truth — JavaScript reads and writes it via `document`, `element.querySelector`, `element.textContent`, `element.append`, `element.addEventListener`, etc.

When you "see HTML in the Elements panel," you're seeing the DOM serialized for display, not the HTML you originally wrote.

### The browser is the runtime

JavaScript in the browser has access to *Web APIs* exposed by the host: `fetch`, `localStorage`, `IntersectionObserver`, `WebSocket`, `crypto.subtle`, etc. None of these are part of the JavaScript language; they're *the platform*. MDN documents them all.

## The request/response model

```
Browser                                       Server
   │                                              │
   │  GET /index.html                             │
   ├─────────────────────────────────────────────►│
   │                                              │
   │  200 OK + HTML                               │
   │◄─────────────────────────────────────────────┤
   │                                              │
   │  Browser parses HTML, finds <link>/<script>, │
   │  issues more requests in parallel...         │
   ├─────────────────────────────────────────────►│
   │                                              │
   │  CSS, JS, images, fonts...                   │
   │◄─────────────────────────────────────────────┤
   │                                              │
   │  Page interactive. JS runs.                  │
   │  fetch('/api/...')                           │
   ├─────────────────────────────────────────────►│
   │                                              │
   │  JSON response                               │
   │◄─────────────────────────────────────────────┤
```

Two things to internalize:

- **HTTP is stateless.** Every request stands alone. State is reconstructed on each request via cookies, tokens, or rebuilding from the database.
- **The first response is just HTML.** All subsequent loads (CSS, JS, images, API calls) are separate requests. The Network panel makes this concrete.

## The toolchain

Modern web dev has a (large) set of tools. The minimum useful set:

| Tool | What it does | When you need it |
|---|---|---|
| **Node.js** (or Bun) | JavaScript runtime outside the browser | The moment you install anything via npm |
| **npm / pnpm / bun** | Package manager | Same |
| **Vite** | Dev server + bundler | Any project beyond a single `index.html` |
| **TypeScript** | Static types over JS | After your second JS project |
| **Prettier** | Code formatter | Day one — kills bikeshedding |
| **ESLint** | Static analysis | Once a project has > ~5 files |
| **Browser dev tools** | Inspection / debugging | Every session, forever |
| **Git** | Version control | Day one |

Tools you *don't* need yet: webpack (Vite is fine), Babel (TS handles it), monorepo tooling, Storybook, micro-frontends, Module Federation, edge runtimes, anything with "enterprise" in its name.

## Frameworks: when and which

A framework manages the *DOM-as-output-of-state* problem. You pick one when:

- You're rendering > ~20 dynamic elements that depend on shared state.
- You're starting to manually rebuild big DOM subtrees on every change and feeling dirty about it.
- You need routing.

Defaults:

- **React** — biggest ecosystem, biggest job market, most docs and AI training data. Default unless you have a reason.
- **Svelte / SvelteKit** — smaller, simpler mental model. Excellent if React's mental model annoys you.
- **Solid** — React syntax with fine-grained reactivity. Niche but elegant.
- **Vue** — coherent, popular outside the US/UK. Smaller in North America.

Skip Angular unless joining a team that uses it.

## State: where it lives

This is the corollary of the mental model on the [index page](./index.md). Web bugs are *almost always* "state in the wrong box."

| Box | Lifetime | Use for |
|---|---|---|
| URL (path + query) | Per page load; shareable; back/forward works | Anything the user might bookmark or share |
| DOM | Until next render | Form input values (sometimes — see below) |
| JS variable / framework state | Until reload | UI state: open menus, hover, optimistic updates |
| `sessionStorage` | Until tab closes | Trivial cross-page-but-same-tab state |
| `localStorage` | Until manually cleared | User preferences, draft text |
| Cookie | Bound to domain; sent with every request | Session tokens (HTTP-only, Secure) |
| IndexedDB | Same as localStorage; structured | Large client-side data, offline apps |
| Server session | Per logged-in user | Authentication |
| Database | Forever | Truth |
| CDN / browser cache | Per cache headers | Performance only — never the source of truth |

The first question for any UI bug: *which box is this state in, and which box do I think it's in?*

## Essential browser dev tool moves

| Action | How |
|---|---|
| Open dev tools | `Cmd+Opt+I` (mac) / `Ctrl+Shift+I` |
| Inspect specific element | `Cmd+Shift+C`, click element |
| Disable cache while open | Network tab → "Disable cache" |
| Throttle network | Network tab → throttling dropdown |
| Pause on any exception | Sources tab → pause-on-exceptions button |
| Edit and re-run a request | Network → right-click → "Replay XHR" or "Edit and Replay" |
| Audit performance | Lighthouse tab → "Analyze page load" |
| Inspect React component tree | Install [React DevTools](https://react.dev/learn/react-developer-tools) |

## Where to go next

- [Tutorial](./tutorial.md) — Levels 1 → 5.
- [Best Practices](./best-practices.md) — once you've finished Level 1, skim this for the conventions.
