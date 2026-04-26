# Best Practices — FL Studio

## Project organization

### Name and color everything
- Rename channels and mixer tracks (`F2`) the moment you create them. "Channel 17" is technical debt.
- Color-code by element type (drums orange, bass purple, vocals red, synths blue, FX gray). The Mixer becomes scannable at a glance.
- Group related tracks via Mixer routing (drum bus, vocal bus, synth bus). Bus processing > per-channel processing for cohesion.

### One project per song; one folder per project
```
projects/
  2026-04-26_house-track/
    project.flp
    samples/         # bespoke samples for this project
    stems/           # exported stems
    masters/         # final WAV/MP3
    notes.md         # what you tried, what worked
```
- The `samples/` folder beside the project survives moves and shares.
- Always save with **Save As Zip Loop Package** when sharing or archiving — bundles all referenced samples.

### Templates
- Save a starter `template.flp` with your standard mixer routing, master chain, and frequently-used plugins. New projects start from copy.
- Different templates per genre if your workflows differ (one for house, one for hip-hop, one for pop).

## Mixing habits

### Gain staging is non-negotiable
- Every individual track should peak at -12 to -6 dBFS. NOT 0 dB.
- Headroom prevents your master bus from being slammed into a limiter from track 1.
- Use the mixer's peak indicator to check; reduce track gain (not the fader — the input gain on the channel) if hot.

### Reference tracks
- Add 2–3 commercial tracks in your genre to a Mixer insert (route an audio clip through it).
- A/B at matched perceived loudness (turn yours up to match theirs, NOT the other way).
- Compare:
  - Kick weight and click
  - Bass body and warmth
  - Vocal presence
  - High-end air
  - Stereo width

### Mix on the speakers/headphones you'll judge from
- Switch between systems (open-back headphones, closed cans, laptop speakers, car) at every milestone.
- A mix that sounds great on one system and bad on three is broken.

### Don't mix on the same day you wrote
- Distance helps judgment. Sleep on it.
- You're not a producer when writing; not a writer when mixing. Switch hats deliberately.

## Performance

### CPU
- Heavy synths (Serum, Diva, Massive X) are CPU intensive. **Freeze tracks** (right-click Mixer track → "Freeze" or render to audio) on completed parts.
- Bounce ambient pads to audio early — saves CPU and lets you process the audio with effects.
- Watch the CPU meter (top-right of FL); 70%+ is danger zone.

### Memory
- Sample libraries (Spitfire, Native Instruments) eat RAM. Disable unused articulations.
- 16 GB RAM is comfortable; 32 GB+ if you're loading sample-heavy orchestral.

### Latency
- Lower buffer = less latency, more CPU, more risk of crackle.
- Recording: low buffer (128 samples, ~3 ms).
- Mixing: high buffer (512–1024 samples) for stability.
- Switch dynamically as needed.

## Plugin discipline

### Don't be a preset hopper
- Preset diving is procrastination dressed as research.
- Pick a small set of synths (one workhorse, one weird, one preset library) and learn them deeply.

### Resist plugin acquisition syndrome
- The DAW's stock plugins do 90% of what's needed.
- Premium plugins (FabFilter Pro-Q 3, Pro-C 2, ValhallaVintageVerb) are worth it once you've outgrown stock — not before.
- Free plugins worth knowing: TDR Nova, TDR Kotelnikov, Valhalla Supermassive, Vital (synth), iZotope Vinyl.

## Workflow

### Limit your first session
- 30 minutes max for the first session of a new track.
- Output: 8 bars of *something*, even rough. End with a save.
- Long opening sessions let perfectionism kill the seed.

### Write first, mix later
- Resist the urge to fine-tune EQ on bar 8 of a 32-bar arrangement. Get the arrangement done first.
- The mix follows from finished arrangement. Don't put the cart before the horse.

### Bounce when in doubt
- If a synth patch is *almost* right, bounce it to audio and move on. You can always go back to the MIDI later if needed.
- Audio is faster to mix than 12 layered synths recalculating every play.

### Capture every fragment
- Even loops you'll never use go in a `_sketches/` folder. Six months later you'll find gold.
- Voice-memo melody ideas before you forget them.

## Collaboration

- Share `.flp` only when the recipient has the same plugins. Otherwise stems.
- Use **Save As Zip Loop Package** to bundle samples.
- Document the project (`notes.md`) — BPM, key, intent, what's missing.
- Stems for vocalists/external mixers: 24-bit WAV, individual tracks, dry (no master bus processing) unless asked.

## Common pitfalls

1. **Effect on a channel does nothing** — channel not routed to a Mixer track.
2. **Mixer faders set to 0 dB on every track** — guarantees clipping. Pull faders down to make room.
3. **Adding a limiter to "fix" a bad mix** — limiters fix nothing; they only mask. Fix the mix first.
4. **Using sidechain on everything** — too much pumping kills musicality. Reserve for kick + bass and maybe pad.
5. **Recording at 48 kHz when your samples are 44.1 kHz** — sample rate conversion happens silently and degrades quality. Pick one and stick with it.
6. **Saving over the only copy** — work in versioned files (`song_v01.flp`, `song_v02.flp`). Disk space is cheap.
7. **Loud monitoring** — fatigues your ears in 20 minutes. Mix at conversation level (~70 dB SPL).
8. **Skipping mastering** — exporting an unmastered project sounds 40% worse on streaming. Even a basic master (EQ + bus comp + limiter) helps.
9. **Not labeling stems before export** — recipients curse you when they get `Track 1.wav`, `Track 2.wav`...
10. **Genre confusion** — using house mixing techniques on a hip-hop track. Each genre has its own conventions; reference within-genre.

## Habits of strong producers

- **Daily 30 min, even if just sketching.** Production muscles atrophy fast.
- **Always finish.** Even bad finished tracks teach more than abandoned good ones.
- **Reference relentlessly.** Compare your work to commercial reference at every step, not just at the end.
- **Master your stock plugins** before buying premium. You can produce a hit on stock-only.
- **Listen to the master on real systems.** Car speakers, AirPods, friend's home theater. Production rooms lie.
- **Keep a reference library** of 20 commercial tracks per genre you produce in. They're your sonic standard.
- **Critique your own work weekly.** Not "is it perfect" but "is it shipped, and what did I learn." Shipping is the metric.
