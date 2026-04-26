# Blender — Quickstart (30 minutes)

If you have 30 minutes today, do exactly these three things. Don't read the rest of the wiki yet.

!!! tip "If you only do one thing"
    Do step 2. Modeling without internalizing modal navigation is the #1 source of beginner frustration.

---

## 1. Install + open + orbit (5 min)

- Download Blender 4.x from [blender.org/download](https://www.blender.org/download/).
- Open it. Default scene: a cube, a camera, a light.
- Practice: middle-mouse drag to **orbit**, Shift+MMB to **pan**, scroll to **zoom**.
- Press `Numpad 1`, `3`, `7` for front/side/top views. Press `Numpad 5` to toggle ortho/perspective.
- Press `Numpad .` to **frame** the selected object (or `Home` to frame all).

If you don't have a numpad, enable *Edit > Preferences > Input > Emulate Numpad*.

---

## 2. The modal mental model (15 min)

This is the single concept that separates Blender confusion from fluency.

- **Object Mode** (default) — you select and transform whole objects.
- **Edit Mode** (`Tab`) — you edit the *insides* of the selected mesh: vertices, edges, faces.

Practice:

- Select the cube. Press `G` (grab/move), then `X` to constrain to X-axis, then type `2`, Enter. The cube moves 2 units on X.
- Press `R` (rotate), `Z`, `45`, Enter. Rotated 45° around Z.
- Press `S` (scale), type `1.5`, Enter. Scaled 1.5×.
- Press `Tab` — now you're in Edit Mode, seeing vertices.
- Press `1` for vertex select, `2` for edge select, `3` for face select.
- Select all vertices (`A`). Press `E` to extrude. Move the mouse, click to confirm.
- Press `Tab` to go back to Object Mode.

You just used the four most important keys: `Tab`, `G`, `R`, `S`. Every workflow extends from these.

---

## 3. Save and revisit (10 min)

- `Ctrl+S` — save your file. Pick a folder you'll find again.
- Close Blender. Reopen the file. Confirm everything's there.
- Open `File > New > Default` to wipe the scene; then `Ctrl+Z` repeatedly to confirm undo works.

---

## What's next

- **Tomorrow (10–20 min):** read [Usage](./usage.md) sections "Modes" and "Essential keyboard shortcuts." Try the shortcuts in a sandbox cube.
- **This week:** start [Tutorial Level 1](./tutorial.md#level-1--navigation-selection-and-the-default-cube). Do not skip ahead.
- **Anki users:** import the [Blender shortcuts deck](../../anki/blender.csv) — 5 minutes of daily review will internalize modal shortcuts in 2 weeks.

Set a calendar reminder for tomorrow. The single biggest factor in Blender progress is *daily 20 minutes* — not weekend marathons.
