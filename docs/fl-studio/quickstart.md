# FL Studio — Quickstart (30 minutes)

If you have 30 minutes today, do exactly these three things. By the end you'll have a 4-bar loop that loops cleanly. That's a finished thing.

!!! tip "Use the trial"
    Don't buy first. Download the free trial from [image-line.com](https://www.image-line.com/fl-studio/) — full functionality except saving. Decide if FL fits before paying.

---

## 1. Install + tour the four windows (10 min)

- Download FL Studio trial from [image-line.com](https://www.image-line.com/fl-studio/). Install. Launch.
- You'll see a default project. Press **F5** (Playlist), **F6** (Channel Rack), **F7** (Piano Roll), **F9** (Mixer). Toggle each.

The four core windows:

| Window         | Shortcut | What it does                                          |
|----------------|----------|-------------------------------------------------------|
| Channel Rack   | F6       | Step sequencer + channel list (instrument slots)      |
| Piano Roll     | F7       | Note editor for any channel (right-click channel → Piano Roll) |
| Playlist       | F5       | Timeline — arrange patterns + audio clips             |
| Mixer          | F9       | Routing, effects, levels                              |
| Browser        | F8       | Files, samples, presets                               |

These five shortcuts (F5–F9) are the only navigation you need on day one.

---

## 2. Make a 1-bar drum pattern (10 min)

In the **Channel Rack**:

- You'll see channels labeled "Kick", "Clap", "Hat", "Snare" (default project).
- The grid to the right is the **step sequencer** — 16 steps per bar, each step a 16th note.
- Click cells to enable steps:
  - **Kick** — click steps 1, 5, 9, 13 (every quarter note — four-on-the-floor)
  - **Clap** — click steps 5, 13 (the backbeat — beats 2 and 4)
  - **Hat** — click every step (1–16) for constant 16ths
- Press **Spacebar** to play. You hear a basic 4-on-the-floor groove.
- Adjust tempo at the top toolbar — try 120, 128, 90 BPM and feel the difference.

You just programmed a beat. That cell grid is the same workflow that built most of EDM.

---

## 3. Add a bassline and arrange (10 min)

- In the Channel Rack, click the **+** at the bottom → search "FL Keys" → Add. A piano channel appears.
- Right-click the FL Keys channel name → **Piano Roll**. The Piano Roll opens.
- Click in the grid to add notes. Try a simple bassline: C2 (held 2 beats), G1 (1 beat), A1 (1 beat). Each note is a 16th-note slot; you can drag to extend.
- Press Space to play. You hear drums + bass.

Now arrange:

- Press **F5** for the Playlist. You see "Pattern 1" already auto-laid down.
- Drag the right edge of Pattern 1 to extend the loop to 4 bars (4 repeats).
- Press Space. Your beat loops 4 bars. **Save the project** (`Ctrl+S`) — name it `2026-04-26-first-loop`.

You've made and saved your first FL Studio project. The mental model — patterns in the Channel Rack/Piano Roll, arranged on the Playlist — is the entire engine.

---

## What's next

- **Tomorrow:** read [Usage](./usage.md), focusing on "Channels vs Mixer Tracks" (the #1 source of FL confusion).
- **This week:** start [Tutorial Level 1](./tutorial.md#level-1--first-16-bar-loop) and follow the [12-week schedule](./practice-schedule.md).
- **Anki users:** import [fl-studio.csv](../../anki/fl-studio.csv) — keyboard shortcuts and native-plugin reference.
- **MIDI keyboard?** Connect it now. Options > MIDI Settings > Input → enable your device. Direct piano input into the Piano Roll is 5× faster than the mouse.

!!! warning "Common first-day frustration"
    "I added an effect to my bass and nothing changed." Cause: the bass channel isn't routed to a Mixer track yet. In the Channel Rack, click the channel's name → set its *Channel settings > Output* to a numbered Mixer track (e.g., "Insert 1"). Now effects placed on that Mixer track affect the bass. This routing step trips up everyone — see [Usage](./usage.md#channels-vs-mixer-tracks).
