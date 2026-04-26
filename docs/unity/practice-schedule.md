# Unity — 12-Week Practice Schedule

20–30 minutes daily, 5 days a week. Designed to take you from zero to a small finished game by the end of the quarter.

## Week 1 — Editor and lifecycle

- [ ] Day 1: [Quickstart](./quickstart.md)
- [ ] Day 2: Hierarchy/Inspector/Project drills — create + name 5 GameObjects
- [ ] Day 3: Read MonoBehaviour lifecycle (Awake, Start, Update, FixedUpdate, OnEnable)
- [ ] Day 4: `[SerializeField]` private vs public; pin a Transform reference via Inspector
- [ ] Day 5: GetComponent vs cached reference; benchmark in your head why caching wins

## Week 2 — Input and movement

- [ ] Day 1: Install Input System package; restart editor
- [ ] Day 2: Create InputActions asset; bind Move (Vector2) to WASD + left-stick
- [ ] Day 3: Generate C# class; wire to a player script
- [ ] Day 4: Rigidbody-driven movement (`linearVelocity` in `FixedUpdate`)
- [ ] Day 5: Add jump via `is_action_just_pressed` equivalent + ground check raycast

## Week 3 — Physics and collisions

- [ ] Day 1: Layers and the Collision Matrix in Project Settings
- [ ] Day 2: Triggers vs collisions; `OnTriggerEnter` vs `OnCollisionEnter`
- [ ] Day 3: Raycasts for ground check, line-of-sight, mouse picking
- [ ] Day 4: `RequireComponent`, `[ExecuteAlways]`, attribute drills
- [ ] Day 5: Force application — AddForce, AddTorque; understand why `linearVelocity` is sometimes better

## Week 4 — Project: simple top-down collector

- [ ] Build the [Level 2 collector](./tutorial.md#level-2--a-real-game). Pickups + score + UI label. Ship it.

## Week 5 — Prefabs and ScriptableObjects

- [ ] Day 1: Create 3 Prefab variants (base enemy → goblin/orc/troll, mesh + stats overrides)
- [ ] Day 2: ScriptableObject for `Item` data; Create asset; reference in inventory
- [ ] Day 3: ScriptableObject event channel — IntEvent — emit + subscribe across two scripts
- [ ] Day 4: Refactor your collector to use SOs for items & a channel for score-changed
- [ ] Day 5: Compare: with-singleton vs with-channel; which would you pick again?

## Week 6 — Scenes and game state

- [ ] Day 1: Create MainMenu and Game scenes; add to Build Profiles
- [ ] Day 2: SceneManager.LoadScene; pass data between scenes via SO
- [ ] Day 3: PlayerPrefs for simple persistence (volume, last name)
- [ ] Day 4: JsonUtility for save/load to `Application.persistentDataPath`
- [ ] Day 5: Pause menu (Time.timeScale = 0); UI overlay via CanvasLayer pattern

## Week 7 — UI Toolkit

- [ ] Day 1: Read [UI Toolkit example](./examples.md#6-ui-toolkit-health-bar)
- [ ] Day 2: Build a HUD UXML/USS — score + health bar
- [ ] Day 3: Bind script via `UIDocument`
- [ ] Day 4: Add a settings panel with sliders
- [ ] Day 5: Compare with uGUI (Canvas) — when would you pick which?

## Week 8 — Animation and AnimationController

- [ ] Day 1: Animator + Animator Controller; states for idle/walk/run
- [ ] Day 2: 1D Blend Tree on Speed parameter
- [ ] Day 3: Trigger Jump from script; transition conditions
- [ ] Day 4: Apply Root Motion vs scripted movement — when to use which
- [ ] Day 5: Animation events; call methods at frames

## Week 9 — Performance and pooling

- [ ] Day 1: Open the Profiler. Run your game. Identify a single frame's time breakdown
- [ ] Day 2: Build IObjectPool<T> for bullets; replace Instantiate/Destroy
- [ ] Day 3: Eliminate per-frame allocations (no string concat in Update without reason)
- [ ] Day 4: Static batching + GPU Resident Drawer in URP
- [ ] Day 5: LOD groups on a high-poly mesh; observe draw calls drop

## Week 10 — Audio and polish

- [ ] Day 1: AudioSource + AudioClip; 2D vs 3D Spatial Blend
- [ ] Day 2: AudioMixer with groups (Music, SFX, Master); volume sliders
- [ ] Day 3: One-shot pooling for SFX
- [ ] Day 4: Camera shake on damage (Cinemachine Impulse Source)
- [ ] Day 5: Particle systems for hit feedback

## Week 11 — Build and ship

- [ ] Day 1: Build Profiles; produce a Standalone Windows or Mac build
- [ ] Day 2: WebGL build; test in browser
- [ ] Day 3: Player Settings — name, icon, splash, version
- [ ] Day 4: Address performance issues you find in the build (always different from editor)
- [ ] Day 5: Upload to itch.io as a draft; **journal the experience**

## Week 12 — Project: polish and release

- [ ] Polish a single small game from the quarter to "shippable" — title screen, audio, pause, settings, credits, build. Release on itch.io even as private link.

---

## After Week 12

- **Bigger ambition?** Pick a 6-month project. Define scope tightly — *small finished* > *big unfinished*.
- **Multiplayer?** Netcode for GameObjects (NGO) or Mirror.
- **DOTS/ECS?** Only after shipping a classic-MonoBehaviour game.
- Cross-reference [Mental Models](../mental-models.md) — Unity prefabs ↔ Godot scenes ↔ Blender node groups; same idea.
