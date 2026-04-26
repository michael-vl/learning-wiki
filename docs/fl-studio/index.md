# FL Studio

Image-Line's FL Studio — a pattern-based DAW with a unique workflow, top-tier Piano Roll, and the industry's best lifetime-update policy. Cross-platform (Windows + macOS).

!!! tip "If you only do one thing"
    **Make and finish a beat in your first session**, even if it's bad. FL Studio's pattern-based workflow rewards short feedback loops; trying to "learn it properly" before producing anything is the dominant failure mode.

!!! note "When FL Studio fits"
    Best for: beat-driven genres (hip-hop, EDM, trap, house, future bass), pop/R&B production, sound design. Capable of any genre, but its idioms are fastest in pattern-based workflows. For long-form recording (live band tracking, scoring to picture) Logic / Pro Tools / Cubase are better defaults.

## Scope

- The four core views — Channel Rack, Piano Roll, Playlist, Mixer.
- Patterns vs audio clips; how arrangement actually works.
- Native instruments (FLEX, Sytrus, Harmor, FL Keys, 3xOsc, Patcher) and effects (Fruity Limiter, Parametric EQ 2, Maximus, Fruity Compressor).
- VST/VST3/AU plugin integration.
- Recording MIDI and audio; comping vocals.
- Mixing — bus routing, sends, automation.
- Mastering options inside FL or via external chain.
- Exporting and sharing.

## Sections

1. [Quickstart](./quickstart.md) — install + first beat in 30 minutes
2. [Usage](./usage.md) — interface, file formats, plugin handling, common gotchas
3. [Tutorial](./tutorial.md) — Level 1 (first 16-bar loop) → Level 5 (full release)
4. [Practice Schedule](./practice-schedule.md) — 12-week checkable plan
5. [Examples](./examples.md) — concrete recipes (sidechain, lead synth, vocal chain)
6. [Best Practices](./best-practices.md) — project organization, mixing habits, performance
7. [Learning](./learning.md) — channels, courses, sample sources

## Editions and pricing (current)

| Edition          | Use case                                | Notes                                       |
|------------------|-----------------------------------------|---------------------------------------------|
| **Fruity**       | MIDI-only — no audio recording          | Cheapest; fine for purely electronic        |
| **Producer**     | Audio recording + automation clips      | Sweet spot for most users                   |
| **Signature**    | Producer + extra plugins (Sytrus, Hardcore, Pitcher, etc.) | Most popular paid tier  |
| **All Plugins Bundle** | Everything Image-Line sells       | Overkill unless you specifically use the bundled plugins |

**The lifetime free updates policy** is FL's killer feature — buy once, every future version is included. No subscription, no Insiders model, no version-locked content. Unique in the DAW market.

There's also a free **trial** with full functionality except project saving — perfect for evaluating before purchase.

## Prerequisites

- Working understanding of music basics (notes, chords, rhythm, time signature). If you don't have this, read the [Music topic](../music/) Tutorial Levels 1–2 first.
- A computer with at least 8 GB RAM (16 GB+ comfortable), an SSD, and either built-in or a USB audio interface.
- Optional but strongly recommended: a MIDI keyboard. The Piano Roll is FL's centerpiece and direct MIDI input is far faster than mouse entry.

## The mental model

FL Studio is built on a **two-layer architecture**:

1. **Patterns** — small, repeatable musical units. Drum loop, bass line, chord stab, vocal phrase. Created in the Channel Rack (step sequencer) and Piano Roll.
2. **Playlist** — the timeline where patterns and audio clips are arranged into a song.

This decouples "writing a part" from "arranging a song" — different from Logic / Pro Tools / Reaper, where everything happens on a single timeline. Patterns are FL's superpower for beat-driven music; they're also why some genres feel awkward in FL (long evolving compositions can be done, but the workflow assumes you don't always need that).

The other key distinction: **Channels (Channel Rack)** ≠ **Mixer Tracks**. A channel is an instrument or sample slot; a mixer track is a routing destination with effects. You explicitly route channels to mixer tracks. Forgetting this is the #1 source of FL Studio confusion ("why isn't my reverb doing anything?").

Once you internalize *patterns + playlist* and *channels route to mixer tracks*, the rest is learning the keyboard shortcuts and the native plugins.
