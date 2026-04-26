# Blender Shaders & Nodes — Quickstart (30 minutes)

If you have 30 minutes, do exactly these three things.

!!! tip "Prerequisite"
    Comfortable in Blender Object/Edit Mode. If not, do the [Blender Quickstart](../blender/quickstart.md) first.

---

## 1. Open the Shading workspace (5 min)

- Open Blender. Click the **Shading** tab at the top.
- Layout: 3D viewport on top, Shader Editor on bottom.
- Default cube has a default material. Click `New` if it doesn't.
- You see two nodes: `Principled BSDF` → `Material Output`.
- Set viewport shading to **Rendered** (top-right of viewport, or `Z` → Rendered).

---

## 2. The "node = function" mental model (15 min)

A shader is a *function* called per shaded pixel. Each node is a function call; sockets pass values.

- `Shift+A` → *Texture* → *Noise Texture*. Drag onto canvas.
- `Shift+A` → *Converter* → *ColorRamp*.
- Connect: `Noise Texture > Fac` → `ColorRamp > Fac` → `Principled BSDF > Base Color`.
- Move the ColorRamp's color stops; the cube updates live.

You just built a procedural texture chain. The **viewer node hotkey** (`Ctrl+Shift+click` on any node) lets you preview any intermediate value — the most useful debugging tool in node editing. Try it.

---

## 3. Make it a reusable group (10 min)

- Select the Noise + ColorRamp.
- Press `Ctrl+G` to group them. The viewport now shows just one node ("Group") plus the Principled BSDF.
- Press `Tab` to enter the group. Set up Group Input/Output sockets:
  - Drag from the noise's Scale → Group Input. Now Scale is exposed externally.
  - Drag the ColorRamp output to a Group Output color socket.
- `Tab` out. The group node now has a `Scale` input and a `Color` output, named.
- Rename the group to "Procedural Color v1" in the N-panel.

You've made a reusable function. Drop it into any future material.

---

## What's next

- **Tomorrow:** read [Usage](./usage.md), focusing on "Sockets and data types" and "How a shader is evaluated."
- **This week:** start [Tutorial Level 1 — first PBR material](./tutorial.md#level-1--your-first-pbr-material). Follow the [12-week schedule](./practice-schedule.md).
- **Anki users:** the [shader nodes deck](../../anki/blender-shaders.csv) covers the 30 most-used nodes by name and purpose.
