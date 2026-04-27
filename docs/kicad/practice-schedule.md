# KiCad — Practice Schedule

PCB design is **project-paced**, not hour-paced. Unlike Blender or piano, you can't make incremental progress on a board for 15 minutes and feel it — boards are integration projects where the value lands at the end. So the schedule below is structured around *finishing* small things on a regular cadence.

!!! tip "Working rule"
    Order one board per month. Even if it's trivial. The act of paying $5 and waiting two weeks for fabrication closes the feedback loop in a way that simulation cannot.

## Daily (10–20 min) — pick one

- [ ] Watch one [Phil's Lab](https://www.youtube.com/@PhilsLab) or [Robert Feranec](https://www.youtube.com/@RobertFeranec) video at 1.25× speed.
- [ ] Read one section of the [Usage](./usage.md) page and try the shortcuts in a sandbox project.
- [ ] Open a finished board (yours or an open-source one) and trace one signal from schematic to board on paper.
- [ ] Read one page of an IC datasheet; identify the recommended land pattern and decoupling.
- [ ] Anki: 5 min on schematic and PCB shortcuts.

## Weekly (2–3 hours) — pick one

- [ ] Make progress on the current Tutorial level.
- [ ] Recreate a circuit from a YouTube video as a schematic; ERC clean.
- [ ] Browse one open-source hardware project on [GitHub](https://github.com/topics/kicad) or [LCSC EasyEDA Open Source](https://oshwlab.com); read the schematic and identify three design choices.
- [ ] Write a custom symbol + footprint for a part you might use later.
- [ ] Run DRC on an old project, fix everything, and re-export.

## Monthly — *order a board*

This is the keystone. Every month, send Gerbers somewhere — even if the board is silly. The constraints are:

- DRC clean, no warnings.
- Silkscreen has the date and your initials.
- You can name every footprint and explain why you chose it.
- You documented the project in a one-paragraph README in the project folder.

Cost is ~$5–15 + shipping at JLCPCB or PCBWay. Two weeks delivery time = a deadline.

## Quarterly — *assemble a board*

Get one board to actually power on. Solder it yourself or pay for assembly. Take a photo. The first time a board powers up correctly is the moment electronics goes from "interesting" to "addictive."

## Anti-pattern checklist

Don't do these:

- [ ] Spend > 1 week on a single Tutorial level. Order what you have, iterate next round.
- [ ] Optimize a board for fabrication you'll never order. The point of the constraints is the order.
- [ ] Switch design tools every two weeks. KiCad is sufficient for ~99% of hobby and small-product work.
- [ ] Watch tutorials without opening KiCad. Passive learning here is especially low-value.

## Tracking

Keep a `boards.md` in your projects folder with one line per board:

```
2026-01  blink              5×  trivial, all worked
2026-02  attiny-board       5×  USB-C polarity wrong, fixed in rev2
2026-03  mic-preamp         5×  picked up clock noise, learned the lesson
2026-04  rp2040-dev         5×  worked first try, kept on desk for a year
```

The list is the metric, not the hours.
