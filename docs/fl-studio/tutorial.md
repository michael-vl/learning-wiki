# Tutorial — FL Studio Beginner to Advanced

Five levels.

---

## Level 1 — First 16-bar loop

**Goal:** make a loop that loops cleanly. End-to-end. Imperfect is fine.

1. New project. Set tempo (Ctrl+T or top toolbar) to your target genre's tempo:
   - Hip-hop / trap: 70–95 (or 140–170 with half-time feel)
   - House: 122–128
   - Drum & bass: 170–180
   - Lo-fi / chill: 70–85
   - Pop: 90–120
2. **Drums** in Channel Rack. Use default channels or drag samples from Browser. 4 bars.
3. **Bass** — add FL Keys or 3xOsc; right-click → Piano Roll. Write 4 bars.
4. **Chords** — add another FL Keys; Piano Roll. Write 4 bars of a 4-chord progression (try [I–V–vi–IV from Music examples](../music/examples.md#1-the-four-core-pop-progressions)).
5. **Lead/melody** (optional) — another instrument; melody over the chords.
6. Route each channel to its own Mixer track (top-left of Channel Rack channel; set 1, 2, 3, 4...).
7. In the Playlist, lay the pattern down for 4 repeats = 16 bars.
8. Hit play. **Save as `2026-04-26-loop-01.flp`**.

You've made a loop. Repeat across the next few sessions, varying tempo, genre, instruments. Quantity over quality at Level 1.

---

## Level 2 — Arrange a full song

**Goal:** turn loops into a song with intro, verse, chorus, bridge, outro.

### Use multiple patterns

- Pattern 1: Drums (verse — sparser kick)
- Pattern 2: Drums (chorus — full kick + claps + hats)
- Pattern 3: Bass main
- Pattern 4: Bass variation (chorus — adds octave)
- Pattern 5: Chords (full)
- Pattern 6: Lead melody
- Pattern 7: Drum fill (1 bar, end of section)

### Arrange on the Playlist

```
Bars:  | 1-4  | 5-12  | 13-20 | 21-28 | 29-36 | 37-40 |
Section: Intro| Verse | Chorus| Verse2| Chorus| Outro |

Pattern lanes:
  Drums:  -    P1     P2     P1     P2     -
  Bass:   -    P3     P4     P3     P4     -
  Chords: P5   P5     P5     P5     P5     P5
  Lead:   -    -      P6     P6     P6     -
  Fills:        P7    P7     P7     P7
```

This is the common "drop sections in/out" technique. Songs grow by adding/removing pattern lanes across the timeline.

### Listen all the way through. Twice.

Note where it gets boring or repetitive. Add or subtract:
- Drum fills before section changes (1-bar variation patterns).
- Risers / sweeps before drops (build tension).
- Filter automation (chorus opens up; verse is low-passed).
- Vocal chops, stab samples, percussion fills.

Save: `2026-04-26-song-arrangement.flp`.

---

## Level 3 — Mixing fundamentals

**Goal:** make individual elements sit together; nothing fights, everything is audible.

### Set up the mixer

- Each instrument routed to its own Mixer insert track. Name them (`F2`).
- Group similar elements onto bus tracks: e.g., all drums route to "Drum Bus" (right-click track → Route to → "Drum Bus"); same for vocals, synths.
- Master gets the final processing only.

### Order of mixing operations (rough)

1. **Gain stage** — set every track to peak around -12 to -6 dBFS (NOT 0 dB or close). Headroom matters.
2. **EQ** — subtractive first. Carve unwanted frequencies (low-cut everything except bass and kick around 80–120 Hz).
3. **Compression** — even out dynamics. Start with vocals (3:1 ratio, fast attack ~10ms, release ~80ms, 3–6 dB GR).
4. **Saturation** — add harmonic content where things sound thin (Soundgoodizer, Fruity Saturator, third-party).
5. **Reverb / Delay** — sends, not inserts. Create one or two send buses (e.g., "Plate Verb", "Long Delay") and route from instrument tracks.
6. **Stereo image** — pan things off-center (kick/bass/lead vocal stay center; everything else spreads).
7. **Master bus** — gentle bus compression (1.5–2:1, slow attack, ~2 dB GR) + Maximus or Fruity Limiter for final loudness.

### Reference

A/B against commercial tracks at matched perceived loudness. If your kick is buried compared to the reference, your kick is too quiet (or your bass is too loud). Mix to **match the reference**, not to taste alone.

---

## Level 4 — Production techniques

**Goal:** the techniques that make modern productions sound modern.

### Sidechain compression
- Place Fruity Limiter (or Fruity Compressor with a sidechain input) on the bass mixer track.
- Right-click compressor's "Sidechain" — pick the kick's mixer track as input.
- Set ratio 4:1, attack 1ms, release 100ms, threshold so kick triggers ~6 dB GR.
- Now the bass ducks every time the kick hits — you hear both, not one over the other. The "house pump."

### Parallel compression (NY drums)
- Send the drum bus to a parallel track via Mixer routing.
- Heavily compress that parallel (10:1, fast attack, 10+ dB GR).
- Blend the parallel under the dry. You get sustain and weight without crushing transients.

### Layering
- A "lead" is rarely one synth. Layer 2–4: a sub-octave for body, a main body, a brightness layer (saw or noise), maybe a percussive transient.
- Each layer gets its own EQ to occupy a different frequency band.

### Vocal chain (rough order)
1. **Subtractive EQ** — high-pass at 80–100 Hz; cut mud at 200–400 Hz; notch any harshness around 2–4 kHz.
2. **De-esser** if sibilance is harsh.
3. **Compressor** — first pass, fast (3:1, 5ms/80ms, 4 dB GR).
4. **Compressor** — second pass, slow (2:1, 30ms/200ms, 2 dB GR). Two stages > one heavy.
5. **EQ** — additive shaping (3 dB shelf at 8 kHz for "air", small bump at 200 Hz for warmth).
6. **Send** to plate reverb + slap delay (return at -15 to -10 dB under the dry).

### Automation
- Right-click any knob → "Create automation clip" → adds to Playlist.
- Edit the curve in the Playlist.
- Use for filter sweeps, volume rides, send levels through a song. Automation makes static mixes feel alive.

### Bouncing stems
- Right-click a Mixer track → "Render to file" or use File > Export > with stems checked. Get individual track WAVs aligned to project start.
- Useful for handing to mix engineers or for collaborating across DAWs.

---

## Level 5 — Mastering and releasing

**Goal:** finish a track to release standard.

### Mastering basics

You're balancing loudness, dynamics, frequency balance, stereo, and tonal cohesion. Mastering ≠ "make it loud."

Master chain order (typical):

1. **Subtle EQ** — fix any obvious frequency imbalance (cut 250 Hz mud; small high shelf if dull).
2. **Bus compressor** — 1.5:1, very slow attack, 1–2 dB GR. Glue, not pump.
3. **Multi-band processor (Maximus)** — separate compression per band; tame highs without dulling.
4. **Limiter** — Fruity Limiter or external; ceiling -1.0 dBTP, gain reduction such that loudness target is hit.
5. **Reference and check on multiple systems** — laptop speakers, car, phone, headphones. If it sounds wrong on ONE system, fix it.

### Loudness targets (LUFS Integrated)

- **Spotify, Apple Music, YouTube**: -14 LUFSi. They normalize loud masters down anyway.
- **Tidal, Amazon HD**: -14 LUFSi.
- **CD / club**: -10 to -8 LUFSi.
- **Ambient / classical**: -16 to -20 LUFSi.

Use a free LUFS meter (Youlean Loudness Meter). Don't push past your target — over-loud masters get penalized by streaming services.

### Export

- File > Export > WAV.
- 44.1 kHz, 16-bit (or 24-bit if you'll do a separate mastering pass elsewhere).
- "Disable maximum polyphony" off, "Tail" on (let reverbs ring out).
- Save to `_masters/` folder; name `track-name_v01_master.wav`.

### Release

- **DistroKid / TuneCore / CD Baby** — distributors that put your track on Spotify, Apple, Amazon, etc. ~$20–40/year for unlimited uploads. Royalties go to you.
- **Bandcamp** — direct sales, you set price + tip jar. Friendly to indie artists.
- **SoundCloud** — community, easy to share, lower discovery than streaming.
- **YouTube** — upload as Art Track or Music video. Discoverability surface.
- **Itch.io** — for games-related music.

Register songs with a PRO (ASCAP, BMI, SESAC in US) for performance royalties. Register with a publisher / Songtrust for sync royalties. These are real money over time if your music gets used.

---

## What "advanced" means in FL

- You finish a track from idea → released master in one week of focused work.
- Your mixes translate well across systems.
- You have a recognizable sonic signature — your kick sound, your sidechain feel, your vocal chain.
- You can produce in ≥3 distinct genres at acceptable quality.
- You've shipped at least 5 finished tracks publicly.

The shipping habit dominates. Most "FL Studio learners" never finish anything because they're chasing tutorials. Make your *finishing* practice deliberate; the production skill follows.
