# Usage — Unity

## Editor anatomy

A default Unity layout has these dockable windows:

- **Hierarchy** — the scene tree. Lists every GameObject in the active scene.
- **Scene view** — 3D editor for placing and tweaking objects.
- **Game view** — what the camera will render at runtime; play mode runs here.
- **Inspector** — properties of whatever is selected (a GameObject, a Prefab, an asset).
- **Project** — the asset browser. Mirrors the `Assets/` folder on disk.
- **Console** — log output, warnings, errors at runtime and in the editor.

Less-used but important:
- **Animation** / **Animator** — animation clip editor and state machine.
- **Profiler** — perf data; learn it earlier than you think you need to.
- **Lighting** — global illumination, light probes, sky.
- **Package Manager** — install official packages and your asset-store assets.
- **Build Profiles** (Unity 6) — replaces *Build Settings*; per-platform configurations.

## Scene view navigation

| Input                        | Action                          |
|------------------------------|---------------------------------|
| Right-mouse drag             | Look (free orbit)               |
| Right-mouse + WASD           | Fly mode                        |
| Middle-mouse drag            | Pan                             |
| Scroll                       | Zoom                            |
| Alt + LMB drag               | Orbit around selection          |
| F                            | Frame selected                  |
| Shift+F                      | Lock view to follow selected    |
| 1/2/3/4/5                    | Tool: Hand, Move, Rotate, Scale, Rect, Transform |
| Q/W/E/R/T/Y                  | Same tools (default Unity)      |
| Ctrl+P                       | Toggle Play mode                |

## Project structure

The `Assets/` folder is yours. Unity manages `Library/`, `Logs/`, `Temp/`, `obj/`, `UserSettings/` — those should be in `.gitignore`.

A sane base structure:

```
Assets/
├── _Project/             # underscore for sort order
│   ├── Art/
│   │   ├── Materials/
│   │   ├── Models/
│   │   ├── Textures/
│   │   ├── VFX/
│   ├── Audio/
│   ├── Prefabs/
│   ├── Scenes/
│   ├── Scripts/
│   ├── Settings/         # render pipeline assets, input actions
│   └── UI/
└── Plugins/              # third-party
```

Group by **functional domain** (Player, UI, Inventory) inside Scripts/, not by C# pattern (Interfaces/, Managers/). The latter is an antipattern that ages poorly.

## MonoBehaviour lifecycle

Every script on a GameObject runs through this lifecycle:

1. **Awake()** — when the GameObject is loaded; before any Start. Use for self-initialization.
2. **OnEnable()** — every time the GameObject/component is enabled.
3. **Start()** — once, before the first Update; after all Awakes have run.
4. **FixedUpdate()** — at the physics tick rate (default 50 Hz). Use for physics (Rigidbody, AddForce).
5. **Update()** — once per frame. Game logic, input.
6. **LateUpdate()** — after all Updates. Camera follow, anything that depends on positions set this frame.
7. **OnDisable()** — when disabled.
8. **OnDestroy()** — when destroyed.

**Order between objects:** within the same lifecycle event, order is undefined unless you set Script Execution Order in Project Settings.

**Coroutines:** `StartCoroutine(MyRoutine())` runs an `IEnumerator` over multiple frames with `yield return` for waits.

```csharp
IEnumerator FadeOut() {
    var color = renderer.material.color;
    for (float t = 0; t < 1; t += Time.deltaTime) {
        renderer.material.color = Color.Lerp(color, Color.clear, t);
        yield return null; // wait one frame
    }
}
```

## The Inspector and serialization

Public fields and `[SerializeField] private` fields show in the Inspector. This is how you wire references in the editor.

```csharp
public class Player : MonoBehaviour {
    [SerializeField] float moveSpeed = 5f;
    [SerializeField] Transform spawnPoint;
    [SerializeField] AudioClip jumpSound;
}
```

**Serializable types** include primitives, Vector*, Color, AnimationCurve, references to UnityEngine.Object subclasses, and your own classes/structs marked `[Serializable]`.

**Don't make everything public.** Use `[SerializeField] private`. Public exposes the field to other scripts; serialized doesn't have to.

## Prefabs

A **Prefab** is a saved GameObject template. To create one: drag a GameObject from the Hierarchy into the Project. You now have an asset.

- **Instances** of a prefab appear blue in the Hierarchy.
- Edit instance overrides in the Inspector — they show as **bold** with a left-edge bar.
- *Apply / Revert* propagates instance changes to the source prefab, or vice versa.
- **Prefab Variants**: a child prefab with overrides that you can save as its own asset. Use for "all enemies share base prefab; goblin/orc/troll variants override mesh and stats."
- **Nested prefabs** are supported and routine — a Player prefab can contain a Weapon prefab as a child.

## Scripting essentials

```csharp
using UnityEngine;

public class Mover : MonoBehaviour {
    [SerializeField] float speed = 5f;

    void Update() {
        var input = new Vector3(
            Input.GetAxis("Horizontal"),
            0,
            Input.GetAxis("Vertical"));
        transform.Translate(input * speed * Time.deltaTime);
    }
}
```

Note `Time.deltaTime` — multiply movement by it so speed is per-second, not per-frame.

For input, **prefer the new Input System** (Window > Package Manager > Input System). It supports rebinding, multiple devices, and modern controller layouts. The legacy `Input.GetAxis` is fine for prototypes but not for shipped games.

## Useful types and shortcuts

- `Vector3.Lerp(a, b, t)` — linear interpolation.
- `Mathf.Clamp01(x)` — clamps to 0–1.
- `Quaternion.LookRotation(forward)` — rotation that faces a direction.
- `Physics.Raycast(...)` — line-of-sight, ground checks, click-to-target.
- `Coroutine` for time-based sequences; `Task` and `await` for proper async (with care — see [best-practices](./best-practices.md)).

## Common gotchas

- **"My script doesn't run."** Is the GameObject active? Is the component enabled? Is the script attached at all?
- **"NullReferenceException on a [SerializeField]."** You declared the reference but didn't drag anything into it in the Inspector.
- **"Movement is jittery."** You're moving in `Update` but the renderer interpolates against physics in `FixedUpdate`. Move via Rigidbody in `FixedUpdate`, or set Rigidbody Interpolation to *Interpolate*.
- **"Editor changes don't survive Play mode."** Play mode is a sandbox — changes during Play revert when you stop. Edit before pressing Play, or copy values out before stopping.
- **"My prefab instance doesn't update."** You overrode the field on the instance. Right-click the field → *Revert*.
- **"Compilation errors but I can still play."** No, you can't. Unity refuses to enter Play mode if any script has compile errors. Check Console.
