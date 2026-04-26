# Usage — Software, Hardware, Setup

## Notation software

For writing music down on a staff:

| Tool             | License             | Best for                                    | Notes                                          |
|------------------|---------------------|---------------------------------------------|------------------------------------------------|
| **MuseScore 4**  | Free, open source   | All-purpose notation                        | Genuinely good; the default recommendation     |
| **Dorico Pro**   | Paid (~$580 perpetual) | Professional engraving, complex scores  | Best engraving; steeper                        |
| **Sibelius**     | Subscription        | Schools, established workflow               | Avid product; pricing is unfriendly             |
| **Finale**       | Discontinued (2024) | Don't pick this for new projects            | Long-time standard; now sunsetting             |
| **Flat.io**      | Freemium, web       | Quick collaboration, light scores           | Browser-based; OK for small things             |

**Default: MuseScore 4.** Free, capable, has a good marketplace of pieces (musescore.com) for finding scores at any level. If you go pro, Dorico is the upgrade path.

## DAWs (Digital Audio Workstations)

For recording, sequencing MIDI, mixing, producing:

| DAW              | License                  | Best for                              | Strengths                              |
|------------------|--------------------------|---------------------------------------|----------------------------------------|
| **Logic Pro**    | $200 (Mac only, one-time)| Songwriters, recording                 | Best value on Mac; great built-in instruments |
| **Ableton Live** | Subscription / paid tiers| Electronic, beat-driven, performance   | Session view is unique; great for sketching |
| **Reaper**       | $60 personal             | Anything; very flexible                 | Cheap, deep, customizable; less polished UX |
| **FL Studio**    | One-time, free updates   | Beat-making, EDM, pattern-based songwriting | See dedicated [FL Studio topic](../fl-studio/) for full coverage |
| **Pro Tools**    | Subscription             | Studio recording, post-production       | Industry standard for tracking; expensive |
| **Cubase**       | Paid, perpetual          | Composers, scoring                      | Strong notation + audio integration     |
| **Studio One**   | Paid tiers, free tier    | All-purpose                             | Clean UX; good defaults                 |
| **GarageBand**   | Free (Mac/iOS)           | First DAW                               | Limited but real; upgrade path to Logic |

**For an intermediate pianist learning to write songs:**
- On Mac: **GarageBand → Logic Pro**.
- On Windows: **Reaper** (cheap, no excuses) or **Studio One Free**.
- For electronic / beat work: **Ableton Live**.

You don't need a DAW to start writing. A piano + a phone voice memo + a notebook is sufficient.

## Hardware

### Keyboard / piano

You already play, so you have one. If you're upgrading:

- **Acoustic piano** — incomparable feel, no latency, no extra cost to play. Tuning ~$200/year.
- **Digital stage / home piano** (Yamaha P-series, Roland FP-series, Kawai ES-series) — weighted hammer action, can go silent (headphones), no tuning needed.
- **MIDI controller** (no built-in sound) — Roland A-88, Komplete Kontrol, Studiologic SL — for use with a DAW.

For composition, anything 88-key with weighted action is sufficient. You don't need synthesizer features; you need a piano feel.

### Audio interface

If you record:
- **Focusrite Scarlett Solo / 2i2** — the standard entry point. ~$120–$200.
- **Universal Audio Volt** series — slightly more, premium feel.
- **MOTU M2 / M4** — well-regarded.

### Headphones (for practice and mixing)
- **Closed-back** for tracking (no bleed): Sony MDR-7506, Beyerdynamic DT 770.
- **Open-back** for mixing/critical listening: Sennheiser HD 600/650/660, AKG K712.

### A condenser mic if you record voice
- **Shure SM7B** (dynamic; podcast/vocal classic).
- **Audio-Technica AT2020 / AT2035** (entry condenser).
- **Rode NT1** (clean, quiet condenser).

## Software for theory and ear training

- **Tenuto** (iOS, ~$4) and **musictheory.net** (free web) — drills for intervals, chords, scales, key signatures. Excellent.
- **EarMaster** — comprehensive ear training, paid; structured curriculum.
- **Functional Ear Trainer** (free apps) — solfege/scale-degree based ear training. Highly effective.
- **iReal Pro** — chord chart playback for jazz/standards practice; great for hearing progressions in any key.
- **Toneable / Soundslice** — slow-down and loop YouTube/score; learn pieces by ear from videos.

## Sheet music and lead sheets

- **MuseScore.com** — community uploads; mixed quality but huge library.
- **IMSLP / Petrucci Music Library** — public-domain classical scores, free.
- **Hal Leonard / Alfred / Schirmer** publishers — paid, vetted, edited.
- **iReal Pro** for jazz/standards (chord charts).
- **Real Book / Real Pop Book / Real Vocal Book** — fake books with thousands of standards.
- **Ultimate Guitar / Songsterr** — chord charts and tabs (popular music; quality varies).

## Practice setup at home

- **Quiet space** with the piano + a chair at the right height (forearms parallel to floor, wrists neutral).
- **Music stand** at eye level.
- **Pencil + manuscript paper** within reach for sketching ideas.
- **Voice recorder** within reach (phone is fine) — capture every promising fragment immediately.
- **Metronome** (physical, app, or DAW).
- **Headphones** for late-night work on a digital piano.
- **A timer** for focused practice blocks (10/20/30 minutes).

## File formats

| Format        | What it is                       | When to use                                       |
|---------------|----------------------------------|---------------------------------------------------|
| `.mscz`       | MuseScore native                 | Working files                                     |
| `.musicxml`   | Open notation interchange        | Move scores between notation programs             |
| `.midi`/`.mid`| MIDI sequence                    | Playback, DAW import; loses engraving             |
| `.pdf`        | Final score                      | Sharing finished scores                           |
| `.wav`/`.flac`| Lossless audio                   | Master recordings, mix exports                    |
| `.mp3`/`.m4a` | Lossy audio                      | Sharing listening copies                          |
| `.aif`        | Apple lossless audio container   | Mac DAW interchange                                |
| `.als`/`.logicx`/`.rpp` | DAW project files       | Working files; not portable across DAWs           |

Always export a PDF of any finished score and keep alongside the working `.mscz`. Always export a `.wav` master and `.mp3` reference of any finished mix.

## Common gotchas

- **Latency** when playing through a DAW — use ASIO drivers (Windows) or a low-buffer-size setting; below ~10 ms total round-trip is good.
- **MIDI channel mismatches** — keyboard sending on channel 1 but DAW listening on channel 2; nothing happens.
- **Score playback ≠ score quality** — MuseScore plays back well enough to verify; it doesn't sound like a real performance.
- **Saving as MIDI loses dynamics, articulations, pedaling.** Use MusicXML for round-tripping notation.
- **Piano tuning drift** with seasonal humidity is normal. Tune in spring and fall.
