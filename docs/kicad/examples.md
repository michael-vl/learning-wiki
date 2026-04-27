# KiCad — Examples

Concrete project ideas, mapped to Tutorial levels. Pick one per level and build it. Avoid the trap of designing a "cool" project before you can finish a simple one.

## Level 1 — Through-hole, single-cell, no semiconductors

- **CR2032 LED throwie** — coin cell + slide switch + resistor + LED. Glue a magnet on the back, stick it to a fridge.
- **Continuity tester** — battery + resistor + buzzer + two probe pads. ESC for a multimeter.
- **Headphone splitter PCB** — 3 × 3.5 mm jacks wired in parallel. Pure DC routing exercise.

Constraints: 2 layers, no SMD, hand-solderable, fits in your palm.

## Level 2 — Microcontroller dev board

- **Bare ATtiny85 board** — USB power, 3.3 V LDO, ICSP header, one button, one LED. Smallest possible useful MCU board.
- **Pico-equivalent** — RP2040 + flash + USB-C + crystal-free reset circuit. The official [RP2040 minimum design example](https://datasheets.raspberrypi.com/rp2040/hardware-design-with-rp2040.pdf) is a great reference.
- **Custom Arduino** — ATmega328P + 16 MHz crystal + USB-serial bridge. Bootload it from a real Arduino.

Constraints: SMD allowed, must include ICSP/SWD header, must include power LED.

## Level 3 — Mixed signal

- **MEMS microphone preamp** — SPH0645 or INMP441 → MCU. Audio over I²S. Forces you to think about ground partitioning.
- **Electret mic + op-amp + ADC** — analog amplification + filter + sample on MCU's internal ADC.
- **Class-D audio amp** — TPA2005 or similar + speaker terminals. Power supply current loops matter here; check the datasheet's layout example.
- **Capacitive touch sensor** — copper electrodes on the silk side, MCU running [TouchLib](https://github.com/AdmarSchoonen/TouchLib) or similar.

Constraints: at least one analog block, separate analog and digital ground islands joined at one point.

## Level 4 — 4-layer

- **USB-PD trigger board** — request 9V/12V/15V/20V from a USB-PD source via something like a CYPD3177. Real product.
- **Ethernet-to-serial bridge** — W5500 or similar + RJ45 magjack + MCU. 4-layer is non-optional once Ethernet is involved.
- **OLED dev board** — RP2040 + I²C SSD1306 + battery management (MCP73831 + LiPo) + USB-C. Daily-driver gadget.
- **STM32 minimum board** — STM32F4 or STM32G4. A ~$5 product-grade dev board.

Constraints: 4-layer, GND and PWR planes on internal layers, JLCPCB stackup-aware impedance for any USB lines.

## Level 5 — Custom symbols/footprints, ready-to-ship

- **Mechanical keyboard PCB** — 60% layout. Forces you to make a custom switch footprint (it's not in the standard libs unless you install [keebio's KiCad libraries](https://github.com/keebio/Keebio-Parts.pretty)) and to think about silkscreen for a thing other humans will see.
- **USB instrument** — small product that does one thing well: a logic-level voltmeter, a frequency counter, a programmable fan controller.
- **Custom badge** — for a conference, club, or just yourself. Forces silkscreen artistry (Edge.Cuts as outline tracing, F.Mask negative-relief logos).
- **A hat / shield for an existing dev board** — Pi HAT, Feather Wing, Arduino shield. Forces you to match someone else's pinout exactly.

Constraints: at least one custom symbol you drew yourself, at least one custom footprint you laid out from a datasheet, at least one 3D model linked from a STEP file.

## Reference open-source designs to read

- **[Adafruit](https://github.com/adafruit)** — most of their boards have public KiCad/Eagle source. Excellent layout style.
- **[Sparkfun](https://github.com/sparkfun)** — same, but with more permissive licensing.
- **[Phil's Lab tutorial repo](https://github.com/pms67)** — the boards from his YouTube series.
- **[Olimex](https://github.com/OLIMEX)** — older but huge variety, including industrial-style designs.
- **[OSHPark Discover](https://oshpark.com/profiles)** — public projects from real users; good for "how would someone else do this?"

Reading a finished schematic is the fastest way to absorb conventions you won't pick up from tutorials.
