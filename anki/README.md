# Anki Flashcard Decks

Spaced-repetition decks for the memorization-heavy parts of each topic. Five minutes a day on the train commute pays off in months.

## How to use

1. Install [Anki](https://apps.ankiweb.net) — desktop is free; mobile (AnkiMobile iOS) is paid one-time, AnkiDroid is free.
2. In Anki, *File > Import* → pick the CSV you want.
3. In the import dialog, set the field separator to comma; map column 1 → Front, column 2 → Back, column 3 → Tags.
4. Pick or create a deck (e.g., "Music — Theory") and import.
5. Daily review takes 5–10 min once you have ~100 cards.

## Decks

- [`blender.csv`](./blender.csv) — modeling shortcuts and key concepts
- [`blender-shaders.csv`](./blender-shaders.csv) — shader/geometry node names and behaviors
- [`unity.csv`](./unity.csv) — MonoBehaviour lifecycle, common types
- [`godot.csv`](./godot.csv) — node types, GDScript syntax, signal API
- [`stock-trading.csv`](./stock-trading.csv) — order types, risk math, tax frameworks
- [`home-building.csv`](./home-building.csv) — code section numbers, design loads, energy values
- [`music.csv`](./music.csv) — intervals, key signatures, chord patterns, modes

## Tips

- **Don't add a card unless you've encountered the concept twice.** Premature cards waste review time.
- **Edit cards aggressively** when you realize the back is unclear or the front is ambiguous.
- **Add your own cards** as you study; the included decks are starters.
- **Suspend cards** that turn out not to matter for your work; don't delete (you might want them later).
- **Daily review > marathon review.** 10 min daily beats 70 min once a week.

## Format

CSV: `front,back,tags` — quoted to handle commas and code:

```
"What does ⌘+S do in Blender?","Save the file","blender,shortcut"
"Define R-21 in IECC CZ 4","Wall cavity insulation R-value 21 minimum","home-building,iecc"
```

Edit in any spreadsheet tool. Re-import to update.
