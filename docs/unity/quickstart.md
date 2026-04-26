# Unity — Quickstart (30 minutes)

If you have 30 minutes, do exactly these three things.

!!! tip "Prerequisite"
    Comfort with C# basics (classes, fields, methods). If C# is new, do a Microsoft *C# Learn* track first — Unity-isms get conflated with C#-isms in your mental model otherwise.

---

## 1. Install + new project (10 min)

- Install **Unity Hub** from [unity.com/download](https://unity.com/download).
- Inside Hub: install **Unity 6 LTS** (latest patch). Include modules: Documentation + your platform's Build Support.
- New Project → template: **Universal 3D (URP)**. Name it. Open.
- Wait for the editor to load (first time can be slow).

---

## 2. The component mental model (15 min)

Everything in a scene is a **GameObject**, which is a *list of components* + a Transform. Behavior comes from attaching components.

- Right-click in Hierarchy → 3D Object → Plane. Right-click → 3D Object → Cube.
- Move the cube up (Inspector > Transform > Position Y = 1) so it sits on the plane.
- Right-click in Project → Create → C# Script → name `Mover`. Double-click to open in your editor.
- Replace contents:

```csharp
using UnityEngine;

public class Mover : MonoBehaviour {
    [SerializeField] float speed = 5f;

    void Update() {
        float x = Input.GetAxis("Horizontal");
        float z = Input.GetAxis("Vertical");
        transform.Translate(new Vector3(x, 0, z) * speed * Time.deltaTime);
    }
}
```

- Save. Back in Unity, drag `Mover.cs` from Project onto the Cube in Hierarchy.
- Press Play. WASD moves the cube.

You just used: a GameObject, a component (Mover script), `[SerializeField]` (exposes `speed` to the Inspector), `Update()` (per-frame), `Time.deltaTime` (frame-rate independence). These five concepts cover ~70% of all Unity scripting.

---

## 3. Save as a Prefab (5 min)

- Drag the Cube from Hierarchy into Project (under Assets). The Cube becomes a Prefab.
- Hierarchy entries reference the prefab; Project asset is the source.
- Edit the Prefab (open the Prefab); change its color (add a Material). All instances update.
- Drag the prefab back into the scene multiple times — instant copies.

This is composition's foundation: save a configured object, reuse it.

---

## What's next

- **Tomorrow:** read [Usage](./usage.md), focusing on "MonoBehaviour lifecycle" and "Prefabs."
- **This week:** start [Tutorial Level 1](./tutorial.md#level-1--hello-cube) and follow the [12-week schedule](./practice-schedule.md).
- **Anki users:** import [unity.csv](../../anki/unity.csv) — MonoBehaviour callbacks, common types.
- **Decide your renderer goal early.** If you're building 2D / mobile / lightweight 3D, stay on URP. HDRP only for offline-quality stylized rendering.
