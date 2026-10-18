# Mult for disting NT: User Manual

*Ormer Modular, made in Guernsey.*

Mult is a chance mult for the disting NT. One input is shared out to four outputs, and each output has its own chance of passing every incoming hit. Feed it a gate or a trigger and each output tosses its own coin: one hit might reach outputs 1 and 4, the next none, the next all of them. It is useful for thinning one clock or drum pattern across several voices.

This is the manual for the Expert Sleepers disting NT plug-in. Version 1.0.0.

## The screen

This is the module's screen, running a port of the plug-in's drawing code, with a simulated input. The compass rose takes the input, and a live scope on its left shows what the input is doing. Four lanes run to the four outputs. A lane that is open carries beads for as long as a signal runs through it, brighter with the level, and its output box follows the level. A lane that is closed stays still. Every hit sends a spark down the lanes: where the hit passes, the spark runs all the way to the output, and where it is blocked, it dies halfway. The bar beside each output is its chance. Click a lane to select it, as the left encoder does. The Clock source idles a little above zero volts, as a real input can. (The chance figures use an approximation of the NT's own font.)

## Controls

Everything is on one screen: four lanes, one per output. There are no pot pages.

| Control | What it does |
|---|---|
| Left encoder, turn | Select a lane (OUT 1 to OUT 4, wrapping). The selected lane is boxed and bright. |
| Right encoder, turn | Set the selected lane's chance, 1% a click. Spin it and it speeds up, so 0 to 100 is not a hundred clicks. |
| Right encoder, push | Set the selected lane's chance back to 100%, the NT's usual "set to default". |
| The three pots, right pot push | Do nothing while Mult's screen is showing, so they never change a parameter you cannot see. |
| Button 2 | Switch to the NT's parameter list, where everything below can be edited, including routing and Threshold. |
| Buttons 1, 3 and 4, left pot push, centre pot push, left encoder push | The NT's own. The left pot push and left encoder push take you back to the overview. |

## How it works

Mult watches the input for hits. A **hit** is the input rising past the **Threshold** (0.5 V by default). After a hit the input has to fall back below half of the Threshold (0.25 V by default) before the next one can count, so noise around a level cannot re-trigger it.

On every hit, each output makes its own choice. It draws a random number from 0 to 99 and passes the hit if the number is below that output's chance. A chance of 63% passes about 63 hits in 100, and 100% passes all of them. The outputs draw separately, so the choices are independent of each other.

- **Pass** means the output carries the input signal, unchanged, until the next hit.
- **Block** means the output sits at 0 V until the next hit (in Replace mode; in Add mode it adds nothing).
- Outputs change only at a hit, so there is no smoothing and no added delay.
- The choices are purely random. There are no seeds and no "fair" or evenly spaced modes. Every hit is independent, and every time the algorithm is loaded the sequence is new.
- Mult is a single channel on the NT: one input, four outputs.

## Gates, triggers, CV and audio

Any signal can go in. What counts as a hit follows from the rule above:

- **Gates and triggers:** one choice per gate or trigger. This is what Mult is for: thinning a clock or a drum pattern.
- **Slow CV:** one choice per cycle of an LFO, or per step of a stepped signal, whenever it rises past the Threshold.
- **Audio:** one choice per waveform cycle. See below.

> **An input that never falls back below half of the Threshold never makes a new choice.** An input that idles a little above zero volts is fine at the default Threshold, up to about 0.25 V. If yours idles higher, or a signal rides between two positive levels, set the Threshold to more than twice the low level and below the high level. Every output keeps its last result until the next hit.

**Audio.** Mult passes audio, and at 100% it passes it cleanly. Below that it makes one choice per waveform cycle, so it randomly drops whole cycles. That adds grit and crackle, even on a pure sine, and you will not hear "a third of the audio". Treat it as a lo-fi effect, not a mute. For musical muting and unmuting, send a gate or a trigger instead. Lower the Threshold toward 0.1 V for the quietest switching point on audio.

## On the disting NT

### Installing

Mult needs [disting NT firmware 1.19 or newer](https://www.expert-sleepers.co.uk/distingNTfirmwareupdates.html).

1. Download `mult-plugin.zip` and unzip it onto the root of the MicroSD card. It puts `mult.o` in `programs/plug-ins/ormermodular/`.
2. Restart the module (or rescan plug-ins from the settings menu).
3. Add an algorithm, then choose **Mult** (tagged Utility).

### Parameters

Every function is a normal NT parameter, listed on two pages: Chance, and Routing.

| Parameter | Range | Default | What it does |
|---|---|---|---|
| Input | a bus, or None | Input 1 | Where the signal comes from. Gates, triggers, CV or audio. With None, nothing happens. |
| Threshold | 0.1 V to 10.0 V | 0.5 V | The level the input must rise past to count as a hit. It must then fall back below half of this before the next hit can count. |
| Out 1 chance to Out 4 chance | 0 to 100%, whole per cent | 100% | The chance that each output passes a hit. 100% passes every hit, so the output is a plain copy of the input; 0% blocks every hit. Also set from the screen. |
| Output 1 to Output 4 | a bus, or None | Output 1 to Output 4 | Where each output goes. With None, that output is not written anywhere. |
| Output 1 mode to Output 4 mode | Add or Replace | Replace | Replace writes the output onto its bus, with 0 V when a hit is blocked. Add sums it onto whatever else is on that bus. |

### Automation and CV

All of it can be mapped to CV, MIDI or i2c and automated through the module's own **Mappings** system, exactly like a built-in algorithm. Map an LFO or a knob to a chance and the pattern thins and fills as it moves. The chances step in whole per cents.

## Field notes

**Thin a drum pattern.** One pattern, four densities. **Input** a clock or a drum trigger · **Out 1** 100% · **Out 2** 70% · **Out 3** 40% · **Out 4** 15% Send the outputs to four voices. The first plays every hit, the others drop more and more of them, differently each time.

**Dice for an envelope.** Each clock either fires the envelope or it does not. **Input** a clock · **Output 1** to the envelope's gate · **Out 1** 50% Raise the chance for a busier line, lower it for a sparser one.

**Density sweep.** Let the pattern breathe. **Out 1** mapped to a slow LFO or a knob in Mappings The output fills and thins as the chance moves.

**A few missing hits.** Humanise a machine-like pattern. **Out 1 to Out 4** all 90% About one hit in ten goes missing, never the same ones twice.

## Troubleshooting

**Mult does not appear in the NT's algorithm list.** Update the module's firmware (Mult needs 1.19 or newer) and check that `mult.o` is inside `programs/plug-ins/ormermodular/`.

**Nothing comes out of an output.** Check that its chance is not 0%, that the Input and that output are set to a bus and not None, and that the input rises past the Threshold. Until the first hit all outputs sit at 0 V.

**The outputs stay open, or stay closed, whatever I set the chances to.** The input is not falling back low enough between hits. It has to drop below half of the Threshold (0.25 V by default). Set the Threshold to more than twice the input's idle level, or check the source really returns low between gates.

**Quiet hits are missed.** The input does not rise past the Threshold. Lower it, down to 0.1 V.

**Audio crackles when I turn a chance down.** That is how Mult treats audio: below 100% it drops random waveform cycles. Use gates or triggers for musical muting.

**I hear a signal twice, or outputs add together.** Two outputs on the same bus in Add mode sum. Keep the default Replace unless you want that.

**The pots do nothing.** By design: while Mult's screen shows, the pots and the right pot push are switched off so you cannot change a hidden parameter. Use the encoders, or press button 2 for the parameter list.

**The screen is still.** It follows the input. With no signal, or Input set to None, it settles.

## Specifications

| | |
|---|---|
| Format | disting NT algorithm, free, closed source |
| Version | 1.0.0 |
| Firmware | 1.19 or newer |
| Input | 1, any bus (or None); gates, triggers, CV or audio |
| Outputs | 4, each on any bus (or None), Add or Replace |
| Chance | 0 to 100 per cent in whole per cent steps, default 100%, one per output |
| Hit | input rises past Threshold (0.1 V to 10.0 V, default 0.5 V); re-arms below half of it |
| Random choices | fresh on every hit, for every output; a new sequence each time the algorithm loads |
| Signal path | passed unchanged: no gain, no smoothing, no added delay |
| Channels | one (the NT has no polyphony) |
| Parameters | 14, on two pages: Chance and Routing |
| Tag | Utility |
