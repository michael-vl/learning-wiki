# Best Practices — Unity

## Project setup

- **Target the latest LTS** (Unity 6 LTS) for new projects unless you have a specific reason. Patch versions ship monthly; minor versions every few months.
- **Render pipeline**: URP for 95% of projects. HDRP only if you need its specific features (volumetric lighting, accurate physical materials, ray tracing). Built-in is legacy — don't start new there.
- **Color space: Linear**. Always. Default for new projects, but verify in Project Settings > Player.
- **Use IL2CPP for builds** (not Mono) on Android, iOS, consoles, and ideally desktop too. Faster runtime, smaller surface for cheating.

## Folder layout

```
Assets/
├── _Project/                   # underscore for sort priority
│   ├── Art/
│   ├── Audio/
│   ├── Prefabs/
│   ├── Scenes/
│   ├── Scripts/
│   ├── Settings/
│   └── UI/
├── Plugins/                    # third-party
└── ThirdParty/                 # alternative naming
```

- Group inside `Scripts/` by **feature** (`Player/`, `Inventory/`, `Combat/`), not by C# pattern (`Managers/`, `Interfaces/`).
- Keep test scenes in `_Project/Scenes/_Sandbox/` — visually separated from real scenes.

## Naming

- **C# classes** PascalCase, files match class names exactly.
- **Variables** camelCase. Private fields use `_` only if your team agrees; not Unity convention by default.
- **Prefabs and SOs** PascalCase: `Player.prefab`, `WoodenSword.asset`.
- **Scenes** PascalCase: `MainMenu.unity`, `Level_01.unity`.
- **Layers and tags**: lowercase or PascalCase, used consistently.

## Code architecture

### Decouple
- **Avoid singletons.** If you must use one, keep it for *true* global services (audio mixer wrapper, scene loader). Game logic should not be globally reachable.
- **Use ScriptableObject channels** (UnityEvent or `System.Action` on a SO asset) for cross-system communication.
- **Reference data, not implementations.** A weapon that takes a `WeaponData : ScriptableObject` is reusable; a weapon that hard-codes its damage is not.

### Composition over inheritance
- Almost no MonoBehaviour should derive from another MonoBehaviour.
- Build behavior by attaching multiple small components, or by composing small POCO classes used by a coordinator MonoBehaviour.

### Small classes
- A MonoBehaviour with 500 lines is a smell. Split into smaller scripts attached to the same GameObject, or into POCO helpers.
- One responsibility per class. "Player" is too broad — `PlayerMover`, `PlayerInputBinder`, `PlayerHealth`, `PlayerAnimator`.

### Async and threading
- Coroutines for time-based sequences (waits, frame steps).
- `async/await` for I/O (asset loading, network). Be careful about Unity's main-thread requirement — most Unity APIs only work on the main thread; `await` resumes there by default in 2021+.
- **Don't do work on background threads** unless you really need it. Burst-compiled jobs (DOTS) are the right answer for parallel work, not raw `Task.Run`.

## Performance

### Rules
- **Profile before optimizing.** Always. Unity profiler in development build, with deep profiling for the spike, then targeted refactor.
- **Avoid allocations in Update** — no `new`, no LINQ, no string concatenation, no boxing.
- **Pool everything spawned at frequency** (bullets, particles, enemies, damage numbers).
- **`GetComponent` is cheap; calling it every frame isn't.** Cache references in Awake.
- **`GameObject.Find` is slow.** Don't.
- **String concat for HUD updates** allocates. Cache the format and use `string.Format` or interpolation only when the value changes, or use a `StringBuilder`.

### Rendering
- **SRP Batcher** + **GPU Resident Drawer** (Unity 6) drastically cut draw calls when shaders are URP/HDRP-compatible.
- **Static batching** for non-moving objects: mark them Static in the Inspector.
- **LODs** (Level of Detail groups) on anything with more than ~5k tris that can be far from the camera.
- **Light baking**: bake lighting for static scenes; use Light Probes for dynamic objects in baked environments.

### Physics
- Set the *Fixed Timestep* (Project Settings > Time) deliberately. Default 0.02 (50 Hz) is fine; 0.0167 (60 Hz) helps if your game logic depends on it.
- Use **layers and the Collision Matrix** to prevent unnecessary collision checks.
- Use **Continuous Dynamic** collision detection only on small fast objects (bullets, projectiles); it's expensive.

## Prefabs and Variants

- **Everything reusable is a Prefab.** A scene with hand-built non-prefab GameObjects is a maintenance nightmare.
- **Prefab Variants** are how you specialize: base "Enemy" prefab → "Goblin" variant overriding mesh and stats.
- **Avoid huge nested-prefab trees.** When a prefab has 7 nested prefabs, finding the override that's broken is painful.

## ScriptableObjects

- For **shared config**: items, weapons, enemy stats, balance values.
- For **events**: ScriptableObject event channels (see [examples](./examples.md#3-scriptableobject-inventory)).
- For **runtime state shared across scenes**: handle with care — SO state persists in editor across Play sessions, which can mask bugs. Reset in `OnEnable()` if needed.

## Version control

- **Use Git with Unity Smart Merge** (UnityYAMLMerge) for `.unity` and `.prefab` merges.
- **Force Text serialization** in Project Settings > Editor.
- **`.gitignore`** must include: `Library/`, `Temp/`, `Logs/`, `Obj/`, `UserSettings/`, `*.csproj`, `*.sln` (these regenerate).
- **Git LFS** for large binaries: `*.png`, `*.psd`, `*.fbx`, `*.wav`, `*.mp4`. Project size explodes without it.
- Branch per feature; PR reviews even on solo projects (forces you to look at your own diff).

## Editor productivity

- **Custom Inspectors and PropertyDrawers** for complex SOs are worth the time once they're used by a designer or non-coder.
- **Editor windows** for tools (level editor, dialog editor). Unity's `EditorGUILayout` is the old API; **UI Toolkit** (`UnityEditor.UIElements`) is the new API. New projects: prefer UI Toolkit.
- **`[ContextMenu]`** on a method gives you a right-click action in the Inspector — quick way to test functions without buttons.

## Debugging

- `Debug.Log`, `Debug.LogWarning`, `Debug.LogError` for stdout-style debugging.
- `Debug.DrawLine` / `Debug.DrawRay` to visualize raycasts in the Scene view (only in Play mode).
- `Gizmos.DrawSphere` etc. in `OnDrawGizmos` / `OnDrawGizmosSelected` for editor-time visualization.
- The **Frame Debugger** (Window > Analysis > Frame Debugger) walks you through every draw call. Educational and bug-finding.
- The **Inspector's tiny lock icon** (top-right) keeps the Inspector showing the same object while you select others — great for drag-drop ops.

## Pitfalls that bite everyone

1. **`OnTriggerEnter` doesn't fire** — neither object has a Rigidbody, or one collider isn't a trigger.
2. **`RaycastHit` always misses** — wrong layer mask; don't pass `~0` carelessly. Use a named LayerMask field.
3. **Frame-rate-dependent gameplay** — forgot `Time.deltaTime`. Movement scales with FPS.
4. **Animator overrides scripted position** — *Apply Root Motion* is on. Disable for code-driven movement.
5. **Build runs differently than editor** — usually a `Resources.Load` path issue, an editor-only `#if UNITY_EDITOR` accidentally protecting needed code, or an asset not included in the build.
6. **Texture import settings wrong** — UI sprites need *Sprite (2D and UI)*, not Default; normal maps need *Normal map*.
7. **Audio source 3D when you wanted 2D** — UI sounds at *Spatial Blend = 0* (2D), world sounds at 1 (3D).
8. **Memory leaks from coroutines** — coroutine still running on a destroyed object will throw.
9. **Garbage collection spikes** — almost always allocations in Update. Hunt with the profiler.
10. **Mobile build crashes on launch** — bad shader, missing IL2CPP architecture, exceeded asset memory budget.

## Habits of strong Unity developers

- **Designers should be able to tune the game without touching code.** SOs, AnimationCurves in the Inspector, exposed sliders.
- **Every system has a sample scene** demonstrating its use in isolation. New developers can open the sample and learn.
- **Every panic-debug session ends in a prevention** — a guard, an assertion, a unit test, or at minimum a comment with a `// CAREFUL:` annotation.
- **Builds happen daily.** A daily standalone build catches platform-specific issues you'd miss running in the editor for weeks.
- **Performance budgets are explicit.** "Frame budget: 16ms. Rendering: ≤ 6ms. Game logic: ≤ 4ms. Physics: ≤ 2ms. Etc." Numbers, not vibes.
