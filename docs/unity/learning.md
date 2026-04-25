# Learning — Unity

A short list. Quality > volume.

## Official

- **Unity Learn** (learn.unity.com). The official curriculum. *Junior Programmer* and *Creative Core* pathways are well-paced for beginners.
- **Unity Manual** (docs.unity3d.com). Reference. The *Scripting* and *Rendering* sections are where the real depth lives.
- **Unity Scripting API** (docs.unity3d.com/ScriptReference) — keep this open in a tab while writing code.
- **Unity Blog** — release notes and engineering posts. The release notes for each Unity 6 patch are valuable; the ecosystem moves fast.
- **Unite talks** on YouTube — annual conference recordings; the architecture, performance, and DOTS deep-dives are gold.

## YouTube — programming

- **Code Monkey** — encyclopedic tutorials with strong code patterns. Especially good for ScriptableObject architecture and Netcode.
- **Tarodev** — tighter, more opinionated, modern C# patterns. The *2D Player Controller* and *Project Architecture* videos are genuinely good.
- **Sebastian Lague** — not a Unity tutorial channel exactly, but his Unity-based math/algorithm explorations teach you more about *thinking* than any straight tutorial.
- **git-amend** — clean architecture talks with full source code; design patterns applied to Unity.
- **Jason Weimann** — long-form courses on YouTube; opinionated, production-experienced.

## YouTube — graphics, shaders, art tech

- **Daniel Ilett** — Shader Graph tutorials, Unity-focused.
- **Ben Cloward** — shader fundamentals, mostly Unreal but the principles transfer; pair with Shader Graph.
- **Acerola** — graphics deep dives, postprocessing, GPU work; high signal.
- **Brackeys** (archived but available) — older Unity videos, still some of the best on basics.

## Books

- **"Unity in Action" (3rd ed.)** by Joe Hocking. Survey of Unity systems. Slightly dated to 2022 conventions but still solid.
- **"Game Programming Patterns"** by Robert Nystrom (free online: gameprogrammingpatterns.com). Engine-agnostic, but every pattern shows up in Unity work.
- **"Code Complete"** (McConnell) — general programming hygiene that prevents the kind of code rot Unity projects tend toward.
- **"Real-Time Rendering"** (Akenine-Möller, Haines, Hoffman) — the rendering bible. Reference, not a read-through.

## Courses (paid)

- **Unity Asset Store > Tutorials** — uneven quality; check reviews.
- **Udemy: GameDev.tv** — *Complete C# Unity Developer* courses. Massive, project-based; good if you want a guided arc.
- **GameDev.tv** also runs courses on Shader Graph, RPG combat, multiplayer.

## Communities

- **Unity Forums** (forum.unity.com) — official, often Unity engineers respond. Search before posting; many bugs are known.
- **r/Unity3D** (and r/gamedev for broader scope).
- **Unity Discord** (link via Unity blog) — closer to live chat support.
- **Unity Discussions** (the new Q&A site replacing UnityAnswers).

## Asset sources

- **Asset Store** (assetstore.unity.com) — curate carefully. Free tier has good basics (POLYGON Starter Pack, Kenney's free assets).
- **Kenney.nl** — free CC0 game art and audio. Use for prototypes; ship with attribution as appropriate.
- **OpenGameArt.org** — community CC0/CC-BY assets.
- **Mixamo** — free character animations (login required). FBX compatible; bring into Unity, retarget if needed.

## Multiplayer

- **Netcode for GameObjects (NGO)** docs at docs-multiplayer.unity3d.com. Sample projects are particularly good.
- **Mirror Networking** (mirror-networking.com) — community alternative; mature.
- **FishNet** — newer community alternative with stronger defaults.

## DOTS / ECS (advanced)

- **Unity DOTS samples** on GitHub (Unity-Technologies/EntityComponentSystemSamples).
- **Code Monkey's DOTS series** — current to Unity 6 ECS API.
- **The official DOTS migration guide** in the manual.

DOTS isn't a beginner topic. Don't approach it until you've shipped a finished game in classic MonoBehaviour Unity.

## Practice rhythms

The most useful thing you can do in your first year is **finish small games**.

- Pong (a weekend).
- Breakout (a weekend).
- A 2D platformer with one level (a week).
- A top-down shooter with three enemy types and a health/score system (a week).
- A small puzzle game with a level select menu (a week).

Five small finished games > one ambitious unfinished game. Each forces a complete loop: design, art (placeholder if needed), code, polish, build, ship to itch.io. The shipping habit is the curriculum.
