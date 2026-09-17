# Expressor

<p align="center">
  <img src="images/hero.gif" width="52%">
  <img src="images/16-rack-mount.jpg" width="39%">
</p>

A tiny 2HP 1U utility module (Intellijel 1U format) that turns an expression pedal into a 0–10V CV source (~9.7V in practice, see [How it works](#how-it-works)). Plug a TRS expression pedal into the `exp` jack, take CV from `out`, and you've got a foot-controlled filter sweep, LFO rate, FX send, or a nice macro controller for your patch. A small LED between the jacks shows you what's happening.

Two stacked PCBs behind a PCB front panel: the **Jack PCB** sits right behind the panel and holds the two jacks and the LED, and the **Main PCB** sits behind that with the actual circuit and the power header (on the silkscreen they're labeled `CtrlBrd` and `MainBrd`).

> [!NOTE]
> If you're in Germany / the EU, I have a bunch of PCB/Panel sets available. Shoot me a message! 

### Three things you should know before you build this

**It uses a 3-pin power connector, not a regular Eurorack ribbon cable.** There's simply no room for a 10-pin header in 2HP 1U. You'll either need the little [3-pin busboard](#3-pin-busboard) from this repo, or the janky jumper-wire hack described in that same section.

**The Main PCB fits in a few different ways, but only one way works.** The power header has to sit behind the green jack, and the components are NOT visible from the back. Flip it 180° and the module won't work. Nothing shorts the power rails in any orientation, but it wasn't the wisest design choice to make it reversible and not label it :D Watch the pictures carefully.

**2HP is tight.** The jacks need to sit perfectly straight — the green one is exactly as wide as the panel, and if it's rotated even slightly you might not be able to fit a module next to it.

> [!TIP]
> Join my [Discord Server](https://glnnk.art/discord) for build support and discussion.

---

## Contents

- [Bill of Materials](#bill-of-materials)
- [PCB & panel files](#pcb--panel-files)
- [How it works](#how-it-works)
- [Assembly](#assembly)
- [3-pin busboard](#3-pin-busboard)
- [Using it](#using-it)
- [License](#license)

---

## Bill of Materials

<p align="center"><img src="images/01-all-parts.jpg" width="70%"></p>

### Module

| Part | Qty | Notes |
|---|---|---|
| Front panel PCB | 1 | [`hardware/panel/`](hardware/panel) |
| Jack PCB | 1 | [`hardware/jack-pcb/`](hardware/jack-pcb) |
| Main PCB | 1 | [`hardware/main-pcb/`](hardware/main-pcb), order it assembled (PCBA), parts listed below |
| [Thonkiconn](https://www.thonk.co.uk/shop/thonkiconn/) stereo jack (PJ366ST, green) | 1 | Expression pedal input |
| [Thonkiconn](https://www.thonk.co.uk/shop/thonkiconn/) mono jack (PJ398SM, black) | 1 | CV output |
| Jack nut | 2 | |
| 0402 LED, color of your choice | 1 | Optional, see [Assembly](#1-led-optional). Bring a spare. They're tiny and tend to yeet into the void |
| 1x3 pin header, SMT, 2.54mm pitch | 2 | Connection between the two PCBs |
| 1x3 pin header, through-hole, 2.54mm pitch | 1 | Power connector |

### Main PCB SMD parts

The BOM and pick-and-place files in [`hardware/main-pcb/`](hardware/main-pcb) are exported from EasyEDA with LCSC part numbers. Order this board assembled (PCBA), e.g. from JLCPCB. The Jack PCB only has the LED on it, so it's cheaper and easier to order that one bare and solder the LED yourself.

| Part | Designator | Footprint | LCSC |
|---|---|---|---|
| TL072CDT dual op-amp | U2 | SOIC-8 | C6961 |
| 1N5819WS Schottky diode | D2, D3 | SOD-323 | C191023 |
| 10µF 25V capacitor | C1, C2 | 0805 | C3853143 |
| 100nF capacitor | C3, C4 | 0603 | C14663 |
| 100kΩ resistor | R1 | 0603 | C25803 |
| 20kΩ resistor | R2 | 0603 | C4184 |
| 2.2kΩ resistor | R3 | 0603 | C4190 |
| 1kΩ resistor | R4 | 0603 | C21190 |
| 1MΩ resistor | R5 | 0603 | C22935 |

### Busboard

| Part | Qty | Notes |
|---|---|---|
| 3-pin busboard PCB | 1 | [`hardware/busboard/`](hardware/busboard) |
| 2x5 Eurorack power header | 1 | Shrouded works too |
| 1x3 pin header, through-hole, 2.54mm pitch | 1–4 | One per 3-pin module you want to power |
| 3-pin female-to-female jumper cable | 1 per module | |
| Kapton tape | | To insulate the back of the busboard |

### What I use with it

- Expression pedal: [Nektar NX-P](https://www.amazon.de/-/en/dp/B07CN7STLC)
- 6.3mm to 3.5mm stereo adapter: [this one](https://www.amazon.de/-/en/dp/B01MZBXTGF)

## PCB & panel files

<p align="center">
  <img src="images/jack-pcb-view.png" width="30%">
  <img src="images/main-pcb-view.png" width="30%">
</p>

Everything's in [`hardware/`](hardware):

- **`hardware/jack-pcb/`** — `gerber_jack-pcb.zip` and `schematic_jack-pcb.pdf`. Two jacks and the LED, nothing else. The LED polarity is marked on the silkscreen (`-` / `+`).
- **`hardware/main-pcb/`** — `gerber_main-pcb.zip`, `schematic_main-pcb.pdf`, `bom_main-pcb.csv` and `pick-and-place_main-pcb.csv`. For PCBA, upload the gerber zip, the BOM and the pick-and-place file.
- **`hardware/panel/`** — `gerber_panel.zip` for the 2HP 1U front panel. `source/` has the KiCad project plus the panel artwork as `.svg`, `.ai` and `.afdesign`, and `jack-pcb-outline-reference.svg`, which I used to line up the panel holes with the Jack PCB. I ordered mine with lead-free HASL and otherwise default settings. ENIG (gold) would look even cooler, but also costs more.
- **`hardware/busboard/`** — `gerber_3pin-busboard.zip` for the busboard, and `gerber_10-to-3pin-adapter_untested.zip`, a single 1:1 adapter from a 10-pin ribbon cable to 3 pins. It needs a 1x3 SMT header and a 2x5 SMT power connector. **I haven't tested this one yet.**

Both PCBs are also on OSHWLab if you want to open and edit them in EasyEDA: [Jack PCB](https://oshwlab.com/info_3955/2hp_exp_copy_copy) / [Main PCB](https://oshwlab.com/info_3955/2hp_exp_copy).

## How it works

The circuit is really simple. A resistor divider (R2/R1) makes a ~10V reference from +12V, and one half of the TL072 buffers it. That buffered reference goes out to the ring of the expression pedal jack. The pedal is just a potentiometer, so its wiper (tip) comes back somewhere between 0V and the reference. The second half of the TL072 buffers that, and the output goes to the CV jack through a 1kΩ resistor and to the LED through 2.2kΩ. R5 (1MΩ) pulls the input to 0V when no pedal is plugged in.

The two Schottky diodes in series with the power rails protect the module if you plug the 3-pin power cable in backwards.

**The output tops out around 9.7V, not a full 10V.** The reverse-protection diode drops ~0.35V off the +12V rail before the divider, so the reference ends up at roughly 11.65V × 100k / 120k ≈ 9.7V.

Your pedal needs to be wired **tip = wiper, ring = reference, sleeve = ground**, which is the most common layout. Some pedals have a polarity switch for this.

## Assembly

### 1. LED (optional)

<p align="center">
  <img src="images/02-led-orientation.jpg" width="48%">
  <img src="images/03-led-soldered.jpg" width="48%">
</p>

The LED is only an indicator for the CV out. If 0402 soldering scares you, just leave it off, since the module works exactly the same without it.

If you wanna add it, **watch the polarity!** The cathode (`-`) goes on the left, pointing towards the large hole between the jacks. Here's a [polarity guide for SMD LEDs](https://lighthouseleds.com/blog/polarity-guide-of-0402-0603-0805-1206-and-most-all-smd-leds.html) if you're not sure which side is which on yours. My boards in these photos don't have the `-` / `+` marks yet, but the gerbers in this repo do.

0402 is super tiny (one was lost during this photoshoot). Easiest way: put some solder on one pad (the right pad if you're right-handed), heat it up again and push the LED in with tweezers. Once it sits right, solder the other pad. Don't apply heat for too long or you'll push it off.

### 2. Bend the jack leads

<p align="center">
  <img src="images/04-jacks-bend-1.jpg" width="48%">
  <img src="images/05-jacks-bend-2.jpg" width="48%">
</p>

Bend the jack leads like in the pictures. They need to be flat against the jack housing, otherwise they won't fit. Also pre-bend them to the sides as shown, otherwise they'll try to twist away.

### 3. Jacks and panel

<p align="center"><img src="images/06-jacks-and-panel.jpg" width="60%"></p>

Place the jacks on the Jack PCB (`E` = green jack, `O` = black jack), put the panel on and use the jack nuts to hold everything in place.

**Make sure the jacks are perfectly straight.** Ideally use clamps (like the Omnifixo) to hold them. Solder one pin on each jack first, check that everything is flush, then solder the rest.

### 4. Trim the jack leads

<p align="center"><img src="images/07-trim-jack-leads.jpg" width="60%"></p>

Use flush cutters to trim the jack leads as flat as you can, otherwise the Main PCB won't sit flush.

### 5. Headers between the boards

<p align="center">
  <img src="images/08-headers-one-pin.jpg" width="48%">
  <img src="images/09-pcb-alignment.jpg" width="48%">
</p>

Take the two SMT headers and solder **only one pin** on each. Don't solder them all yet! Put the Main PCB on and make sure it fits and both headers are perfectly aligned. You can carefully heat up that one pin between the PCB sandwich to nudge a header into place.

Once everything is straight, take the Main PCB back off and solder the rest of the SMT header pins.

### 6. Power header

<p align="center">
  <img src="images/10-power-header-alignment.jpg" width="48%">
  <img src="images/11-power-header-orientation.jpg" width="48%">
</p>

Solder the 1x3 power header onto the Main PCB. It goes on the back side, where the text and the `-12V @ Stripe` mark are. Make sure it's soldered at a right angle.

### 7. Put it together

<p align="center">
  <img src="images/12-done-side.jpg" width="40%">
</p>

Put the Main PCB back on. **The power header sits behind the green jack!** If you get it the wrong way around, the module won't work.

Solder one pin on each header, make sure everything is flush, then solder the rest and trim the pins so they're nice and flush with the PCB.

Use a multimeter to check for shorts between the power pins and GND before you plug it in.

## 3-pin busboard

<p align="center"><img src="images/busboard.jpg" width="60%"></p>

- Solder the 2x5 power connector. If you're using a shrouded one, the notch should point towards the PCB edge. Plug a cable in to double check that the red stripe matches the white line.
- Solder one or more 1x3 headers.
- Put Kapton tape on the back of the busboard and over any unused header pins, so nothing shorts later (especially if your case is made from metal).
- Use a 3-pin female-to-female jumper cable to connect the module. Pay close attention to match the white line on the busboard with the `-12V` mark on the module.

**Janky hack:** if you don't want to order the busboard, use a 3-pin male-to-female jumper cable and push the male end into a regular Eurorack power cable. The 5 rows of 2 pins are: -12V on one end (red stripe side), +12V on the other end, and the three rows in the middle are all GND, any of those is fine. Ideally secure everything with some tape.

## Using it

<p align="center">
  <img src="images/14-rack-sideview.jpg" width="32%">
  <img src="images/15-rack-connected.jpg" width="32%">
</p>

Connect your expression pedal and move it. The LED should go from off to full brightness and the CV output from 0V to ~9.7V. If it doesn't, check your pedal for any settings or adjustments. On my Nektar NX-P I use Mode 1 (switch on the back), and the offset potentiometer on the left needs to be at zero.

Now take the CV output and use it in your patches. It works great as a manual filter control, for LFO speed on an Øchd, as an FX send, or as a macro control routed to multiple destinations.

**Only plug a stereo (TRS) cable into the expression jack.** A mono cable shorts the reference output to ground. It won't break anything (the TL072 is short-circuit protected), but the module won't output anything useful and the op-amp gets warm, so don't leave it like that.

## License

[MIT](LICENSE), for everything in this repo: PCB files, panel artwork and docs.

# The End
I hope this was a fun project and you got through with ease. If you're having difficulties at any point, please reach out. You can join my [Discord Server](https://glnnk.art/discord) for support.
I'd also love to see your creations! Tag me on Instagram or send me a photo to add here.
Check out my other stuff on [YouTube](https://glnnk.art/youtube) or [Instagram](https://instagram.com/glnnk.art).
You can [Buy me a coffee](https://www.paypal.com/paypalme/finnglink) if you've found my work helpful :)
