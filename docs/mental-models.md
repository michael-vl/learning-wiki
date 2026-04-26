# Mental Models — The Hidden Curriculum

The seven topics in this wiki look unrelated. They're not — for someone with engineering training, the same handful of mental models recur across all of them. Recognizing this saves years.

!!! tip "Why this page exists"
    Most learners treat each new domain as if it has nothing in common with anything they already know. That doubles the cost of learning. The opposite move — actively asking "what does this remind me of?" — is one of the strongest accelerators of skill transfer.

---

## 1. Systems thinking — flows, stocks, control

A house's HVAC system, a Godot scene, a Blender Geometry Nodes graph, a trading strategy, and a song's harmonic structure are all **systems**: components that exchange flows under feedback.

| Domain          | Stocks (state)          | Flows (transfers)            | Control (feedback)             |
|-----------------|-------------------------|------------------------------|--------------------------------|
| HVAC (home)     | Indoor air temperature  | Heat in/out via ducts        | Thermostat → equipment         |
| Trading system  | Account equity          | Position P&L, fees, taxes    | Stop-loss → exit               |
| Godot scene     | Node states, variables  | Signals, method calls        | Signals/conditions → behavior  |
| Geometry Nodes  | Geometry data           | Modifications down the graph | Field evaluations              |
| Song harmony    | Tonal "home" (key)      | Chord-to-chord motion        | Cadences resolve tension       |

Once you see this isomorphism, you can use the same diagnostic questions everywhere:
- *What's the steady state, and what perturbs it?*
- *Where does feedback close the loop?*
- *What happens when feedback breaks (saturated, lagged, broken)?*

A stuck thermostat, a runaway trading drawdown, a Godot signal that never fires, a Geometry Node infinite loop, and a song that never resolves are all the same bug shape.

---

## 2. The DAG — directed acyclic graphs everywhere

A surprising fraction of creative software is built on DAGs:

- **Blender Shader Editor** — nodes flow toward `Material Output`.
- **Blender Geometry Nodes** — nodes flow toward `Group Output`.
- **Blender Compositor** — nodes flow toward `Composite`.
- **Unity URP Shader Graph / Godot VisualShader** — same.
- **DAW signal chains** — track → effects → bus → master.
- **Build pipelines** (CI/CD, Cargo, Make, Bazel) — same shape.
- **Dependency graphs** in your home design (foundation supports framing supports MEP supports finishes).
- **A trading strategy execution** — universe → signal → entry → sizing → exit.

If you understand one DAG editor, you understand them all. The differences are vocabulary.

---

## 3. The DSP / signal-and-noise mindset

Your ME background includes signal processing intuition. It transfers:

- **Trading**: returns are mostly noise; edge is a tiny signal you have to detect with statistics. Sample size, multiple-comparison correction, and signal-to-noise reasoning prevent false discovery.
- **Mixing/mastering**: literal DSP — EQ filters, compression, phase, stereo image. The math is identical to vibration analysis you already know.
- **Building science**: heat transfer is a low-pass filter; the building envelope is a thermal capacitance and resistance circuit. Lstiburek's "perfect wall" is just sound RC design with vapor as the third axis.
- **Animation curves** in Blender, Unity, Godot: easing functions are sigmoid filters applied to time. Same math.

The same intuition that says "you can't extract a signal below the noise floor without averaging" applies to "you can't conclude your strategy works from 20 trades."

---

## 4. Composition — small reusable pieces with clean interfaces

| Domain     | The small piece           | The interface                            |
|------------|---------------------------|------------------------------------------|
| Blender    | Node group                | Inputs/outputs by name and type          |
| Unity      | MonoBehaviour / Prefab     | `[SerializeField]` fields, public methods|
| Godot      | Scene                     | Exported variables, signals              |
| Home       | Wall assembly type        | Where it meets foundation, roof, openings|
| Trading    | A signal function          | Inputs (price, volume); output (boolean) |
| Music      | A 4-bar phrase             | Starting key/mode; ending chord          |

Always design the interface (the *outside*) before sweating the implementation (the *inside*). When the interface is right, the inside is replaceable.

This is the deep reason "make a node group even for one-shot materials" appears in the Blender best-practices, "make a prefab" appears in Unity, "make a scene" appears in Godot — they're all the same advice expressed in three vocabularies.

---

## 5. Gradient descent on quality — iterate, don't perfect

Anywhere you're producing creative or designed work, the workflow is:

1. Cheap rough draft.
2. Evaluate against the goal.
3. Improve the worst part.
4. Repeat.

Trying to perfect step 1 before step 2 is the classic engineer trap. It applies the same way to:
- Modeling a character (blockout → refine, not finished-eye → finished-nose).
- Writing a song (full rough demo → revise sections, not perfect verse before touching chorus).
- Designing a house (schematic in 2 hours → critique → schematic v2).
- Building a trading strategy (working backtest with bad metrics → improve weakest assumption).

Short feedback loops dominate everything. The discipline that ships often gets better faster than the one that ships rarely.

---

## 6. Constraint satisfaction — code, budget, time

Every project has hard constraints (gravity, building code, market hours, octave range, frame budget). Designing *toward* constraints, not around them, produces better work:

- **Building code** is a constraint, not a problem; it forces design choices that often turn out to be the right ones (fenestration ratio, egress, structural redundancy).
- **Budget** in trading is account-equity-times-risk-percentage; you can't spend more.
- **Frame budget** in Unity/Godot is 16ms; you can't spend more on any single frame.
- **Singing range** is two octaves; melodies that exceed it are unsingable.

Constraints simplify the design space. Engineers know this; creatives often resist it. Both worlds benefit from the engineer's stance.

---

## 7. Pre-commit, then execute — defeat in-the-moment irrationality

Same fix in different domains:

- **Trading**: bracket order (entry + stop + target placed together) so you don't move the stop in panic.
- **Construction**: change-order process in writing, not verbal "yeah do it" decisions.
- **Songwriting**: define "finished" before starting (e.g., "verse + chorus, demo recorded") so you can't perfectionist-procrastinate forever.
- **Practice**: schedule appears in `now.md` Sunday; you execute Mon–Sat without renegotiating each morning.

The strong move is always to make the rational decision *before* the emotional moment, then bind future-you to it. This is Ulysses contracting himself to the mast across every domain in this wiki.

---

## 8. Bias toward the boring core, satellite the rest

- **Investing**: 80%+ in low-cost index funds, ≤20% in active ideas you actually want to learn.
- **Building**: budget the boring stuff (envelope, structural, MEP) properly; pick finishes within the leftover envelope.
- **Music**: master fundamentals (rhythm, voice leading, hearing chord function) before chasing exotic theory.
- **3D / game dev**: nail your topology and prefab discipline before exploring procedural systems.

In every domain, beginners chase novelty (the satellite) and neglect the core. The *core* is where 80% of returns come from. Boring, repetitive, sometimes unfulfilling — and dispositive.

---

## How to use this page

Reference, not curriculum. When you're stuck in a topic, come back here and ask: *"Which of these eight have I forgotten to apply?"* Most learning impasses are not about the topic itself; they're about a mental model you already know being unconnected.

Link a concrete example back here when you notice the connection in your journal. Over time you build a personal reference of "I figured this out in Blender; the same fix worked in Godot" — that's how cross-domain expertise actually accumulates.
