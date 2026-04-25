# Tutorial — Unity Beginner to Advanced

Five levels. Don't race.

---

## Level 1 — Hello, Cube

**Goal:** make a cube you can move with WASD.

1. Unity Hub → New Project → **Universal 3D (URP)** template, Unity 6 LTS.
2. In the Hierarchy: right-click → 3D Object → Plane (the ground). Right-click → 3D Object → Cube. Move the cube up so it sits on the plane.
3. Add a directional light (default scene has one). Add a camera (default).
4. Right-click in the Project window → Create → C# Script → name it `Mover`.
5. Drag `Mover.cs` onto the cube in the Hierarchy.
6. Open the script (double-click). Replace contents:

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

7. Save. Back in Unity, wait for the script to compile (bottom-right spinner). Press Play. WASD moves the cube.

**Concepts you just touched:** scene hierarchy, components, MonoBehaviour, Input axes, Time.deltaTime, the Inspector field showing `speed = 5`.

---

## Level 2 — A real "game"

**Goal:** a top-down player that collects pickups and increments a score.

1. Replace the cube with a *Capsule*. Add a `Rigidbody`, freeze rotation X/Z (Constraints in the Rigidbody Inspector).
2. Update Mover to use Rigidbody movement:

```csharp
using UnityEngine;

[RequireComponent(typeof(Rigidbody))]
public class PlayerMover : MonoBehaviour {
    [SerializeField] float speed = 5f;
    Rigidbody rb;

    void Awake() => rb = GetComponent<Rigidbody>();

    void FixedUpdate() {
        var input = new Vector3(
            Input.GetAxis("Horizontal"), 0,
            Input.GetAxis("Vertical"));
        rb.linearVelocity = input.normalized * speed
            + Vector3.up * rb.linearVelocity.y;
    }
}
```

3. Add a small sphere, tag it as a pickup (top of Inspector → Tag → Add Tag → "Pickup"; assign).
4. Make the sphere a Prefab (drag from Hierarchy to Project / Prefabs).
5. Scatter copies of the prefab around the plane.
6. Add a `Pickup` script to the prefab:

```csharp
using UnityEngine;

public class Pickup : MonoBehaviour {
    void OnTriggerEnter(Collider other) {
        if (!other.CompareTag("Player")) return;
        ScoreManager.Instance.Add(1);
        Destroy(gameObject);
    }
}
```

7. The sphere needs a *Collider* with `Is Trigger` checked, and either object needs a Rigidbody (the player has one).
8. Tag the player as "Player".
9. Score manager — a singleton, just to ship Level 2:

```csharp
using UnityEngine;
using TMPro;

public class ScoreManager : MonoBehaviour {
    public static ScoreManager Instance { get; private set; }
    [SerializeField] TMP_Text label;
    int score;

    void Awake() => Instance = this;
    public void Add(int n) {
        score += n;
        label.text = $"Score: {score}";
    }
}
```

10. Add a UI Canvas, a TextMeshPro - Text element, drag it to the ScoreManager's `label` field.
11. Press Play. Move into spheres. Watch the score tick up.

**Concepts:** Rigidbody, Trigger colliders, tags, Prefabs, Singletons (avoid in Level 4+, but useful here), TextMeshPro, the UI Canvas.

---

## Level 3 — State, scenes, and the new Input System

**Goal:** menu → game → game over, with proper input bindings.

### Replace `Input.GetAxis` with the Input System

1. Window > Package Manager > Input System (install). When prompted, restart the editor with the new system.
2. Project → Create → Input Actions → name it `PlayerInput`.
3. Open the asset. Add an action map "Gameplay". Add an action "Move", type *Value*, control type *Vector2*. Bind: WASD composite, left stick, etc.
4. Generate C# class: tick *Generate C# Class* in the asset Inspector, Apply.
5. Use it in PlayerMover:

```csharp
using UnityEngine;
using UnityEngine.InputSystem;

[RequireComponent(typeof(Rigidbody))]
public class PlayerMover : MonoBehaviour {
    [SerializeField] float speed = 5f;
    Rigidbody rb;
    PlayerInput input;
    InputAction moveAction;

    void Awake() {
        rb = GetComponent<Rigidbody>();
        input = new PlayerInput();
        moveAction = input.Gameplay.Move;
    }

    void OnEnable() => input.Enable();
    void OnDisable() => input.Disable();

    void FixedUpdate() {
        Vector2 v = moveAction.ReadValue<Vector2>();
        rb.linearVelocity = new Vector3(v.x, rb.linearVelocity.y, v.y) * speed;
    }
}
```

### Multiple scenes
1. File > Save Scene As → "Game".
2. Create new scene → "MainMenu". Add a UI canvas with a "Start" button.
3. Create `MainMenuController` to load the Game scene:

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
public class MainMenuController : MonoBehaviour {
    public void StartGame() => SceneManager.LoadScene("Game");
}
```

4. Build Profiles (formerly Build Settings) → add both scenes to the build list. The MainMenu must be index 0.
5. Wire the Start button's OnClick to `MainMenuController.StartGame`.

### A simple game-over flow
- When player hits a hazard (a red cube with a `Hazard` script), reload the scene or load a "GameOver" scene.

---

## Level 4 — Architecture: events, ScriptableObjects, dependency

**Goal:** stop using singletons. Decouple systems via events and ScriptableObject "channels".

### ScriptableObject as data

```csharp
using UnityEngine;

[CreateAssetMenu(menuName = "Game/Item")]
public class Item : ScriptableObject {
    public string displayName;
    public Sprite icon;
    public int value;
}
```

Right-click in Project → Create → Game → Item. You now have a *data asset*. Use these for: items, enemies, weapon stats, anything that's "data, not a thing in the world."

**Why ScriptableObjects?** Designers can create variants without touching code. They serialize cleanly, version cleanly in Git, and decouple data from runtime logic.

### Event channels (ScriptableObject + UnityEvent)

```csharp
[CreateAssetMenu(menuName = "Game/Events/IntEvent")]
public class IntEvent : ScriptableObject {
    public event System.Action<int> OnRaised;
    public void Raise(int value) => OnRaised?.Invoke(value);
}
```

A "ScoreChanged" channel is a single asset. Anything that wants to *raise* it gets a reference; anything that wants to *listen* subscribes. The score manager and the UI no longer need direct references to each other — they just both reference the channel asset.

This pattern is the foundation of **decoupled architecture** in Unity. It's the alternative to the singleton hellscape that ships in many tutorials.

### The Service Locator vs. Dependency Injection trade

For larger projects, install **VContainer** or **Zenject** as a DI framework. For small/medium projects, ScriptableObject channels + `[SerializeField]` references are enough. Don't over-engineer; introduce DI when a singleton starts hurting.

---

## Level 5 — Performance, profiling, multiplayer, shipping

### Profiling
- Window > Analysis > Profiler. Run in Play mode; record a session.
- Headers to learn: **CPU**, **GPU**, **Rendering**, **Memory**, **Audio**, **Physics**.
- The single most useful skill: identify a single frame's spike, drill into the call tree, find what allocated.

### Common perf wins
- **Don't use `GameObject.Find` or `FindObjectOfType` in Update.** Cache references in Awake.
- **Don't allocate in Update.** No `new`, no LINQ, no string concat in hot paths. Allocation triggers GC, which spikes frametime.
- **Pool objects** (bullets, particles, enemies) instead of `Instantiate`/`Destroy` constantly. Unity ships with `IObjectPool<T>` since 2021.1+.
- **Batch draw calls** — use the SRP Batcher (URP/HDRP do this for you with the right shaders) and the GPU Resident Drawer (Unity 6) for static geometry.
- **Reduce overdraw** in 2D (alpha-blended layers stacked) and complex transparent VFX.
- **Use the Rendering Debugger** (Unity 6) to inspect lighting, transparency cost, post-processing cost.

### Build pipeline
- Build Profiles → make profiles per platform (Standalone Windows, Android, iOS, WebGL).
- For mobile, change Color Space to *Linear* (it should already be), and enable IL2CPP for ARM64. ARMv7 is dead for new builds.
- For WebGL, expect long iteration cycles. Test in browser early, not at the end.

### Addressables
- Move late-loaded assets to the **Addressables** package. Load by string key with `Addressables.LoadAssetAsync<GameObject>("Prefabs/Enemies/Goblin")`.
- This is how you keep build size small and patch content without re-deploying the binary.

### Multiplayer (skim only — full topic on its own)
- **Netcode for GameObjects (NGO)** — Unity's first-party MonoBehaviour-style netcode. Best for small co-op / lobby-style games.
- **Netcode for Entities** — built on DOTS, scales further but a deeper learning curve.
- **Mirror, FishNet** — mature community alternatives; FishNet has better defaults for newer projects.
- All require a transport (Unity Transport, Steam, Epic, etc.) and a relay/host model. Self-hosting requires server build + matchmaking.

### Shipping checklist
- Resolution and aspect ratio handling (Canvas Scaler set right; safe areas on mobile).
- Settings menu (audio sliders, key rebinds — the Input System makes this routine).
- Save / load (PlayerPrefs for small data; binary or JSON for game saves; Steam Cloud / iCloud for sync).
- Localization package for shipping outside English.
- Crash reporting (Unity Cloud Diagnostics, Sentry, Backtrace).
- Telemetry sparingly. Privacy-first; document what you collect.

### What "advanced" means in Unity
You can architect a project that survives a designer adding 200 items, an artist swapping the entire art style, a programmer joining mid-development, and a port to a new platform — without rewriting. That's the bar.
