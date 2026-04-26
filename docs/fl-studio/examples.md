# Examples — FL Studio

Concrete recipes. Rebuild rather than copy.

---

## 1. Sidechain "pumping" bass

The hallmark of house, future bass, and a thousand pop drops. Bass ducks every kick.

```
Setup:
  Channel: Kick     → Mixer Insert 1 ("Kick")
  Channel: Bass     → Mixer Insert 2 ("Bass")

In Mixer Insert 2 (Bass):
  Effect slot 1: Fruity Limiter
    - Click "COMP" tab
    - Sidechain input: right-click input level → "Sidechain to this track from..." → pick Kick (Insert 1)
    - Threshold: -18 dB
    - Ratio: 4:1
    - Attack: 1 ms
    - Release: 100 ms
    - Aim for ~6 dB GR on each kick hit

Hit play. Bass ducks rhythmically with the kick. Adjust release to taste —
shorter = punchier, longer = smoother.
```

Alternative method: **Fruity Peak Controller** routes a signal to *any* parameter. Even more flexible (sidechain filter cutoff, reverb wet, etc.) but more setup.

---

## 2. Lead synth — saw layered with sub

```
Channel 1: 3xOsc
  Osc 1: Saw, Coarse 0
  Osc 2: Saw, Coarse 0, Fine +7 cents (slight detune for width)
  Osc 3: Saw, Coarse 0, Fine -7 cents
  Filter: LP, cutoff 70%, resonance 20%
  Envelope (Volume): A 5ms, D 100ms, S 80%, R 200ms

Channel 2: 3xOsc
  Osc 1: Sine, Coarse -12 (one octave down for sub)
  Osc 2: off, Osc 3: off
  Volume = ~50% of Channel 1

Both routed to same Mixer track ("Lead").

Mixer: Lead track effects:
  1. Fruity Parametric EQ 2 — high-pass at 100 Hz; small bump at 4 kHz for presence
  2. Fruity Reverb 2 — small room, mix 15%
  3. Fruity Delay 3 — 1/8th note, mix 10%, feedback 30%
```

A simple 2-layer lead instantly bigger than a single instance. Add a third layer (noise / white-noise burst at attack) for percussive presence.

---

## 3. Vocal chain (modern pop)

```
Mixer Insert: Vocal Lead

Effects (in order, top to bottom):
  1. Fruity Parametric EQ 2
     - HP at 100 Hz (steeper than default — 24 dB/oct)
     - Cut 250 Hz by -3 dB (mud)
     - Small notch at 3 kHz if harsh on this voice
  2. Fruity De-esser (or third-party FabFilter Pro-DS) — center 6–8 kHz, ~3–4 dB GR on sibilance
  3. Fruity Compressor (first stage)
     - Ratio 3:1, Attack 5 ms, Release 80 ms
     - Threshold to give 4–6 dB GR on loudest words
  4. Fruity Compressor (second stage) — slower
     - Ratio 2:1, Attack 30 ms, Release 200 ms
     - Threshold to give 2 dB GR (catches occasional peaks)
  5. Fruity Parametric EQ 2 (additive)
     - +3 dB shelf at 8 kHz ("air")
     - +1 dB shelf at 200 Hz (warmth — cautious)
  6. Sends:
     - Send 1 → Plate Reverb bus (-12 dB)
     - Send 2 → 1/8 Slap Delay bus (-15 dB)
```

Two compressors stacked is far smoother than one heavy one.

---

## 4. Drum bus glue

```
Routing:
  Kick → Insert 1
  Snare → Insert 2
  Claps → Insert 3
  Hats → Insert 4
  Percussion → Insert 5
  All five route to → Insert 10 ("Drum Bus")

Drum Bus effects:
  1. Fruity Compressor (bus glue)
     - Ratio 1.5:1, Attack 30 ms, Release auto
     - Threshold for 1–2 dB GR on the loudest hits
  2. Fruity Parametric EQ 2
     - High shelf +1 dB at 10 kHz (sparkle)
  3. Fruity Stereo Enhancer
     - Slight stereo widening (only above 200 Hz to keep low end mono)
```

Don't over-process the drum bus. Glue compression should be felt, not heard.

---

## 5. Sound design — pluck patch in 3xOsc

A staple of house/EDM:

```
Channel: 3xOsc
  Osc 1: Saw, Coarse 0
  Osc 2: Saw, Coarse +12 (octave up), Volume -3 dB
  Osc 3: Square, Coarse 0, Volume -6 dB

  Volume Envelope: A 1 ms, D 200 ms, S 0%, R 100 ms (zero sustain = pluck)
  Filter: LP, cutoff 50%, resonance 15%
  Filter Envelope: A 1 ms, D 100 ms, S 0%, R 100 ms (filter closes after pluck)

Effects:
  1. Fruity Reverb 2 — large hall, mix 25%
  2. Fruity Delay 3 — 1/4 note ping-pong, feedback 40%
```

Play 8th-note arpeggios on a minor chord and you've got a future-bass pluck.

---

## 6. Filter sweep automation (build to drop)

```
1. Channel "Lead Synth" routed to Mixer Insert 4.
2. On Insert 4, add Fruity Parametric EQ 2.
3. Right-click EQ band 5 frequency knob → "Create automation clip".
4. In Playlist: the automation clip appears as a new lane.
5. Edit the curve:
   - Bar 16 (start of build): frequency 200 Hz (heavily LP'd)
   - Bar 24 (drop): frequency 22 kHz (fully open)
   - Curve type: exponential (right-click handle → tension)
6. Add a riser sample on top during the build for extra hype.
```

The "filter open" sound is in 80% of EDM drops. Master it once, use forever.

---

## 7. A 4-pattern song skeleton

```
Pattern 1: Drums-verse (sparse kick, no claps)
Pattern 2: Drums-chorus (full kick + clap + hat fills)
Pattern 3: Bass (4-bar riff)
Pattern 4: Chords (4-bar progression)
Pattern 5: Lead melody (chorus only, 4 bars)
Pattern 6: Drum fill (1 bar before each chorus)

Playlist arrangement:

Bar:    1   5   9   13  17  21  25  29  33  37  41  45
        |Intro|Verse|PreCh|Chor|Verse|PreCh|Chor|Bridge|Chor|Out|

Drums (P1/P2/P6):
  Intro:   silence
  Verse:   P1 x 2 bars
  PreCh:   P1 x 2 bars + P6 fill at end
  Chorus:  P2 x 8 bars
  ...

Bass (P3):
  Intro:   silence
  Verse:   P3
  PreCh:   P3
  Chorus:  P3 (but transposed up an octave for energy)

Chords (P4):
  Throughout (or sparsely in bridge)

Lead (P5):
  Chorus only (and bridge with octave variation)
```

Same skeleton serves house, pop, R&B, hip-hop. Genre comes from instrument choice and tempo, not arrangement.

---

## 8. Exporting stems for collaboration

```
File > Export > WAV file
  Tail: ON (let reverbs ring out)
  Disable maximum polyphony: OFF (let it polyphonize properly)
  Save as separate tracks: ON (creates one WAV per Mixer track)
  Sample rate: 44.1 kHz
  Bit depth: 24-bit
  Save into: ./stems/<song-name>/

Result: a folder with one WAV per non-empty mixer track, all aligned to project start.
A collaborator can drop them into any DAW and rebuild the mix from scratch.
```
