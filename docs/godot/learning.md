# Learning — Godot

## Official

- **Godot Docs** (docs.godotengine.org). The official manual + tutorial. The *Step-by-step* tutorial ("Your first 2D game" → "Your first 3D game") is genuinely good — better than most paid courses.
- **Godot Class Reference** — built into the editor (F1 / Help > Search). Treat it as a primary source; nothing is faster than the in-editor docs.
- **Godot YouTube channel** — official talks, including roadmap and feature reveals.

## YouTube — beginner

- **GDQuest** — high-production-value courses and tutorials. Their free *Learn GDScript from Zero* interactive course is excellent.
- **Heartbeast** — patient, project-based 2D tutorials. The action RPG series teaches a complete game arc.
- **PlayWithFurcifer** — clean explanations of mid-tier topics (state machines, dialogue, save systems).
- **Brackeys** — recently moved from Unity to Godot; his new Godot videos are well-paced for newcomers.

## YouTube — intermediate / advanced

- **Bramwell** — UI design and shaders.
- **godotneers** — node and architecture deep dives.
- **Game Dev Artisan** — practical tutorials with strong production focus.
- **Cyberreality / DevWorm / Coding Quests** — varied; sample a few and pick the voice that fits.

## Shaders

- **Godot Shaders** (godotshaders.com) — a community library of shader snippets. Read them; modify them; learn by reverse-engineering.
- **The Book of Shaders** (thebookofshaders.com) — generic GLSL but transfers 1:1 to Godot shaders.
- **Inigo Quilez's articles** (iquilezles.org) — SDFs, noise, raymarching. Foundational.

## Books

- **"Godot 4 Game Development Cookbook"** (Vivien Anglesio / various editions) — recipe-style; useful as a reference once you know basics.
- **"Game Programming Patterns"** by Robert Nystrom (free online) — engine-agnostic, but every chapter applies to Godot.
- **"Game Engine Architecture"** by Jason Gregory — overkill for using Godot, but illuminating if you want to understand what's happening under the hood.

## Communities

- **Godot Forum** (forum.godotengine.org) — official, slow-moving but high-quality.
- **Godot Discord** (link from godotengine.org) — large, active. Help channels are friendly to beginners.
- **r/godot** — fast-moving, lots of show-and-tell, helpful for question-answer matchups.
- **Godot Engine Stack Exchange / GameDev Stack Exchange** — searchable Q&A.

## Asset sources

- **Kenney.nl** — CC0 art and audio packs, a Godot favorite for prototyping.
- **OpenGameArt.org** — community CC0/CC-BY assets.
- **itch.io game assets** — many free or cheap, often Godot-friendly.
- **Mixamo** — free character animations, FBX import works in Godot 4 (or via glTF re-export from Blender).

## Multiplayer

- **Godot's High-level Multiplayer docs** in the official manual — start here.
- **Heartbeast's multiplayer tutorials** — practical 2D online co-op.
- For larger-scale, study existing open-source Godot multiplayer games on GitHub.

## Editor plugins (worth trying)

Install via the AssetLib tab in the editor:

- **Dialogue Manager** (Nathan Hoad) — a complete, scriptable dialogue system. The de-facto standard.
- **Phantom Camera** — Cinemachine-style camera framework for Godot.
- **GodotXTerm** — embed a real terminal in the editor (niche but cool).
- **Beehave** — behavior trees for AI.
- **Godot Jolt** — replaces the default 3D physics engine with Jolt for much better performance and stability (Godot 4.4+ ships Jolt as an option natively).

## Practice rhythms

- **Replicate one tutorial a week** for the first month. Pick small, finishable ones.
- **Re-implement a classic** — Pong, Breakout, Asteroids, Frogger. Each is a 1–2 day project teaching one mechanic deeply.
- **Game jams** — Godot is *the* engine for jams under 72 hours. Itch.io hosts the *Godot Wild Jam* monthly. Three jams in a year teaches more than three months of YouTube.
- **Read other people's projects.** Godot scenes are text — open someone's `.tscn` and `.gd` files, follow the signals, see how they decompose.
