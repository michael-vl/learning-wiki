# Web Development — Quickstart (30 minutes)

If you have 30 minutes today, do exactly these three things. Don't read the rest of the wiki yet.

!!! tip "If you only do one thing"
    Do step 3. The site has to be *online*, on a real URL someone else can visit. A `index.html` on your desktop is not the same skill as a deployed page; the deploy step is the one that compounds.

---

## 1. Make a folder, write one HTML file (5 min)

```bash
mkdir hello-web && cd hello-web
```

Create `index.html` with this exact content:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Hello, web</title>
  <style>
    body { font: 16px/1.5 system-ui, sans-serif; max-width: 40rem; margin: 4rem auto; padding: 0 1rem; }
    button { font: inherit; padding: 0.5rem 1rem; }
  </style>
</head>
<body>
  <h1>Hello, web</h1>
  <p>The current time is <span id="time">—</span>.</p>
  <button id="refresh">Refresh</button>
  <script>
    const el = document.getElementById('time');
    const btn = document.getElementById('refresh');
    function update() { el.textContent = new Date().toLocaleTimeString(); }
    btn.addEventListener('click', update);
    update();
  </script>
</body>
</html>
```

Open it in your browser (double-click the file, or `open index.html` on macOS). Click the button. You just used HTML, CSS, JavaScript, and the DOM API.

---

## 2. Open the dev tools (10 min)

This is the part most beginners skip and pay for forever.

- In the browser, right-click the page → **Inspect** (or `Cmd+Opt+I` / `Ctrl+Shift+I`).
- **Elements** tab — see the live DOM. Edit a `<p>` text inline. Notice the page changes.
- **Console** tab — type `document.title = 'Changed'`, press Enter. Tab title changes.
- **Network** tab — reload the page. See `index.html` load. Click the request, see headers.
- **Sources** tab — find your `<script>`. Click a line number to set a breakpoint. Click the button — execution pauses there.

Every web problem you'll ever debug is solved through one of those four panels.

---

## 3. Put it on the internet (15 min)

Pick one. Both are free for personal sites.

### Option A — Cloudflare Pages (no install)

- Sign up at [pages.cloudflare.com](https://pages.cloudflare.com).
- Click *Upload assets*, drag the folder, name it `hello-web`. Done.
- You get a URL like `hello-web.pages.dev`. Send it to a friend.

### Option B — Vercel CLI

```bash
npm i -g vercel
vercel       # follow the prompts; accept defaults
```

You get a URL like `hello-web-xxxx.vercel.app`. Send it to a friend.

That's it. You shipped a website.

---

## What's next

- **Tomorrow (20 min):** read [Usage](./usage.md) sections "The platform" and "The toolchain."
- **This week:** [Tutorial Level 1](./tutorial.md#level-1--a-personal-site) — extend `hello-web` into a real one-page personal site.
- **Don't yet:** install React, Next.js, Tailwind, or anything fancy. The frameworks make sense only after you've felt the pain they solve.

Set a calendar reminder. Web dev rewards reps; one shipped page is worth ten followed tutorials.
