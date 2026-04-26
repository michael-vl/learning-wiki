# Usage — FL Studio

## The four core windows

### Channel Rack (F6)
The list of every channel in your project. A **channel** = an instrument, a sample, or a generator slot. Each channel has:

- A **step sequencer** row (16 steps by default; resize with right-click).
- **Channel settings** (double-click the channel name) — instrument plugin UI.
- A **mixer track assignment** (the small number left of the channel name) — where this channel routes to in the Mixer.

Add channels via the **+** at the bottom (search/browse for samples or plugins) or by dragging from the Browser.

### Piano Roll (F7)
FL Studio's flagship. Open by right-clicking any channel → *Piano Roll*. Each channel has its own Piano Roll editor.

Key actions:
- Click empty area = add note (length = whatever the last drawn note was).
- Click a note + drag = move; drag right edge = resize.
- Right-click = delete.
- `Ctrl+drag` = select; `Ctrl+A` = select all.
- `B` (brush) / `P` (paint) / `D` (delete) / `S` (slip) tool modes.
- **Strum** (`Alt+S`), **Arpeggiate** (`Alt+A`), **Quantize** (`Q`), **Strum** are in the Tools menu.
- Snap setting (top-right of Piano Roll) controls grid resolution.

### Playlist (F5)
The arrangement timeline. Two layer types:
- **Pattern clips** — placeholder for a Pattern. Resize horizontally to repeat the pattern.
- **Audio clips** — actual recorded or imported audio.
- **Automation clips** — knob/parameter automation lanes.

Different from other DAWs: Playlist tracks are *not tied to channels*. A single Playlist track can hold any pattern or audio. Many users put one pattern per track for clarity, but you don't have to.

### Mixer (F9)
- 99+ insert tracks plus a Master.
- Each insert has 10 effect slots (top-right of mixer panel).
- **Sends** between mixer tracks via right-click → Route to.
- The Master is where final processing (limiter) goes.

Routing channels to mixer tracks: in the Channel Rack, top-left of the channel = the mixer track number. Set explicitly. The default is "Master" (number 0) if not set, which means effects you add elsewhere don't affect that channel.

### Browser (F8)
File and preset browser. Drag samples into the Channel Rack or Playlist directly. Star presets/samples for fast retrieval. Add custom folders via Options > File Settings.

## Patterns

A **Pattern** is a named collection of notes/steps for any number of channels. Default project has Pattern 1.

- **Pattern selector** at the top toolbar (next to the BPM display).
- `+` to create a new pattern; `-` to delete.
- Each pattern remembers per-channel notes. So Channel Rack steps for Pattern 1 are different from Pattern 2.
- Patterns are placed on the Playlist as clips.

Use cases:
- Pattern 1 = drum verse loop.
- Pattern 2 = drum chorus loop (slightly different).
- Pattern 3 = bass riff.
- Pattern 4 = chord stab.
- Then arrange these patterns on the Playlist into verse / chorus / bridge structure.

Alternative workflow: one mega-pattern with everything, edited in the Piano Roll directly. Either works.

## Channels vs Mixer Tracks

The single most important conceptual distinction:

- A **channel** (Channel Rack) generates sound (synth, sampler, sample slot).
- A **mixer track** (Mixer) processes sound — applies effects, sets level, routes to other mixer tracks.

You **must explicitly route** a channel to a mixer track. In the Channel Rack:

- Top-left of each channel: small numeric box = mixer track destination (default 0 = Master, no insert).
- Right-click that box → "Mixer Track" → enter a number.
- Or click and scroll to set.

Once routed, anything on that mixer track's effect slots affects the channel.

**Recommended convention**: name mixer tracks (`F2` to rename) and color-code (`F2` color). Group similar channels onto the same mixer track only if you want shared effects (e.g., all hats on one track for a single hat-bus EQ).

## Plugins

FL supports:
- **Native FL plugins** — bundled, integrated tightly, recall perfectly across versions.
- **VST 2 / VST 3** — cross-platform, the de-facto standard.
- **AU (macOS)** — supported since the macOS port.
- Image-Line plugins ship as both native and VST.

To scan for new plugins: Options > Manage Plugins > Find Plugins. Set search paths first if needed.

To use a plugin as an instrument: in Channel Rack, **+** → All > pick plugin name. To use as an effect: in Mixer, click an effect slot → pick plugin.

### Native instruments worth knowing

- **FLEX** — preset-driven, easy to use; comes with hundreds of free packs. Great for first-pattern leads/pads/basses.
- **FL Keys** — basic piano, lightweight, great for sketching.
- **3xOsc** — three-oscillator subtractive synth; small but mighty for bass.
- **Sytrus** — FM/additive/subtractive hybrid; deep but rewards study. (Signature edition.)
- **Harmless** — subtractive that *sounds* additive. Bright leads, warm pads.
- **Harmor** — additive synth, very flexible. Powerful for sound design.
- **Patcher** — meta-plugin that lets you build chains/macros of other plugins.
- **GMS (Groove Machine Synth)** — multi-osc, performance-friendly.

### Native effects worth knowing

- **Fruity Parametric EQ 2** — primary EQ.
- **Fruity Limiter** — compressor + limiter combo; good for buses and master.
- **Fruity Compressor** — basic comp.
- **Maximus** — multi-band processor (compressor / limiter / expander); great for mastering.
- **Fruity Reverb 2 / Convolver** — reverbs.
- **Fruity Delay 3** — modern delay.
- **Soundgoodizer** — quick "make it loud and bright" — useful but lazy if overused.
- **Edison** — built-in audio recorder/editor.

## File formats

| Format     | What it is                              | Notes                                        |
|------------|-----------------------------------------|----------------------------------------------|
| `.flp`     | FL Studio project                       | Native; not portable to other DAWs           |
| `.fst`     | FL state preset (channel/effect state)  | Snapshots of plugin settings                 |
| `.zip`     | Project zipped with samples (Save As Zip Loop Package) | Best for sharing/backup            |
| `.wav`/`.flac` | Lossless audio                      | Master output, sample import                 |
| `.mp3`/`.m4a`/`.ogg` | Lossy audio                   | Reference exports                            |
| `.mid`     | MIDI                                    | Import/export between DAWs                   |
| `.dawproject` | DAW-portable open format             | Limited, evolving — for cross-DAW work       |

## Recording

### MIDI from a controller
1. Connect controller via USB.
2. Options > MIDI Settings → enable your input device.
3. In Channel Rack, click the channel you want to record into.
4. Open Piano Roll for that channel.
5. In the toolbar, enable **Recording** (the red circle icon, or `R`).
6. Hit play. Played notes record into the Piano Roll.

### Audio
1. Connect interface and mic.
2. Options > Audio Settings → set your interface as input.
3. In Mixer, select an empty insert track. Set its **Input** (top of the channel strip) to your hardware input.
4. Arm record on that track (the small disk icon).
5. Hit record + play. Audio records into the Playlist as an audio clip on the corresponding Playlist track.

### Comping vocals
- Record multiple takes onto adjacent Playlist tracks.
- Use **Slice** tool (S) to chop into sections.
- Drag final pieces onto a comp track.
- For pitch correction: **Newtone** (FL native, Producer+) or external (Melodyne, Auto-Tune).

## Common gotchas

- **"My effect doesn't do anything."** Channel isn't routed to a mixer track. Route it (top-left of Channel Rack channel).
- **"My MIDI controller doesn't trigger anything."** Either the input wasn't enabled in Options > MIDI Settings, or the channel isn't selected in the Channel Rack.
- **"My audio crackles / latency is bad."** Lower buffer size in Options > Audio Settings, but go too low and you get dropouts. Use ASIO drivers (Windows; ASIO4ALL if you don't have a native ASIO driver). On macOS, Core Audio is built-in and good.
- **"Sound stops playing when I switch windows."** Options > General Settings → enable "Auto-export with audio" only matters for exports, but for playback issue: check Options > Audio > "Use polyphonic playback" and "CPU > Multithreaded generator processing" — both default-on, but worth verifying.
- **"My save file got huge."** You're using sample-based instruments without "Memory: Use loaded sample" or you embedded large samples. Use the Browser to point at sample folders instead of dragging-and-saving.
- **"I can't find a sample I dragged into the project."** It's referenced from its original disk location, not embedded. If you move/delete the original, the project breaks. Use **File > Save As Zip Loop Package** to bundle samples for portability.
- **"Pattern length wrong."** The default pattern is 1 bar (16 steps). Use the pattern-length toolbar (or right-click pattern selector) to set 2, 4, 8 bars; or just lay multiple patterns on the Playlist.
- **"Why is the metronome not playing?"** Click the metronome icon in the top toolbar; also enable in Options > Project Settings > "Click while playing".
