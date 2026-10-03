# Mult: VCV Rack manual

Version 2.0.0, 2 HP.

Mult is a small chance mult. One input is shared out to four outputs, and each output has its own chance of passing every incoming hit. Feed it a gate or a trigger and each output tosses its own coin: one hit might reach outputs 1 and 4, the next none, the next all of them. It is useful for thinning one clock or drum pattern across several voices. It is polyphonic, and every channel of every output decides on its own.

## The panel

Mult has one input at the top. Below it, four stages run down the panel: a chance knob, a light, then the output it belongs to.

**Input**

- **IN**: The signal to share out to the four outputs: gates, triggers, CV or audio. Mult watches it for a hit, which is the input rising past 0.1 V. Each hit gives every output a new choice. The input is polyphonic: the outputs carry as many channels as the input, up to 16, and each channel is judged on its own.

**Chance knobs**

- **OUT 1 CHANCE**: Sets the chance, from 0 to 100 per cent in whole per cent steps, that output 1 passes each hit. 100% (the default) passes every hit, so the output is a plain copy of the input; 0% blocks every hit. It applies to every channel of the output. Hover over the knob to read the value, for example "Out 1 chance: 63%". Double-click it to return to 100%.
- **OUT 2 CHANCE**: Sets the chance, from 0 to 100 per cent in whole per cent steps, that output 2 passes each hit. 100% (the default) passes every hit, so the output is a plain copy of the input; 0% blocks every hit. It applies to every channel of the output. Hover over the knob to read the value, for example "Out 2 chance: 63%". Double-click it to return to 100%.
- **OUT 3 CHANCE**: Sets the chance, from 0 to 100 per cent in whole per cent steps, that output 3 passes each hit. 100% (the default) passes every hit, so the output is a plain copy of the input; 0% blocks every hit. It applies to every channel of the output. Hover over the knob to read the value, for example "Out 3 chance: 63%". Double-click it to return to 100%.
- **OUT 4 CHANCE**: Sets the chance, from 0 to 100 per cent in whole per cent steps, that output 4 passes each hit. 100% (the default) passes every hit, so the output is a plain copy of the input; 0% blocks every hit. It applies to every channel of the output. Hover over the knob to read the value, for example "Out 4 chance: 63%". Double-click it to return to 100%.

**Lights**

- **OUT 1 LIGHT**: Flashes (for about 60 ms) when output 1 passes a hit. With a polyphonic input it flashes when any channel of that output passes. It marks the hit, not the time the output spends open, so a long gate shows as one flash at its start.
- **OUT 2 LIGHT**: Flashes (for about 60 ms) when output 2 passes a hit. With a polyphonic input it flashes when any channel of that output passes. It marks the hit, not the time the output spends open, so a long gate shows as one flash at its start.
- **OUT 3 LIGHT**: Flashes (for about 60 ms) when output 3 passes a hit. With a polyphonic input it flashes when any channel of that output passes. It marks the hit, not the time the output spends open, so a long gate shows as one flash at its start.
- **OUT 4 LIGHT**: Flashes (for about 60 ms) when output 4 passes a hit. With a polyphonic input it flashes when any channel of that output passes. It marks the hit, not the time the output spends open, so a long gate shows as one flash at its start.

**Outputs**

- **OUT 1**: Carries the input unchanged while output 1 is open, and sits at 0 V while it is closed. It changes only at a hit and holds its choice until the next one. It has the same number of channels as IN. With nothing patched to IN the output is silent, and after a patch loads it stays at 0 V until the first hit.
- **OUT 2**: Carries the input unchanged while output 2 is open, and sits at 0 V while it is closed. It changes only at a hit and holds its choice until the next one. It has the same number of channels as IN. With nothing patched to IN the output is silent, and after a patch loads it stays at 0 V until the first hit.
- **OUT 3**: Carries the input unchanged while output 3 is open, and sits at 0 V while it is closed. It changes only at a hit and holds its choice until the next one. It has the same number of channels as IN. With nothing patched to IN the output is silent, and after a patch loads it stays at 0 V until the first hit.
- **OUT 4**: Carries the input unchanged while output 4 is open, and sits at 0 V while it is closed. It changes only at a hit and holds its choice until the next one. It has the same number of channels as IN. With nothing patched to IN the output is silent, and after a patch loads it stays at 0 V until the first hit.

## How it works

Mult looks at the input for hits. A **hit** is the input rising past 0.1 V. After a hit the input has to fall back to 0 V or below before the next one can count, so noise around a level cannot re-trigger it.

On every hit, each output makes its own choice. It draws a random number from 0 to 99 and passes the hit if the number is below that output's chance. A chance of 63% passes about 63 hits in 100, and 100% passes all of them. The outputs draw separately, so the choices are independent of each other.

- **Pass** means the output carries the input signal, unchanged, until the next hit.
- **Block** means the output sits at 0 V until the next hit.
- Outputs switch only at a hit, which is just past 0 V, so there is no big step at the switch.
- The choices are purely random. There are no seeds and no "fair" or evenly spaced modes. Every hit is independent, nothing repeats on reload, and nothing about the choices is saved in the patch.

Mult has no other inputs. The four chance knobs are the only controls.

## Polyphony

Each output carries as many channels as the input, up to 16. Every channel of every output decides on its own, so a polyphonic clock comes out as separate random patterns, one per channel. One knob per output sets the chance for all of that output's channels, and an output's light flashes when any of its channels passes a hit.

## Gates, triggers, CV and audio

Any signal can go in. What counts as a hit follows from the rule above:

- **Gates and triggers:** one choice per gate or trigger. This is what Mult is for: thinning a clock or a drum pattern.
- **Slow CV:** one choice per cycle of an LFO, or per step of a stepped signal that rises past 0.1 V.
- **Audio:** one choice per waveform cycle. See below.

> **A signal that never comes back down near 0 V never makes a new choice.** For example, an LFO that stays between 2 V and 5 V rises past 0.1 V once and then never falls back to 0 V, so every output keeps its last result. A signal that stays below 0.1 V never makes a hit at all, and the outputs stay closed.

**Audio.** Mult passes audio, and at 100% it passes it cleanly. Below that it makes one choice per waveform cycle, so it randomly drops whole cycles. That adds grit and crackle, even on a pure sine, and you will not hear "a third of the audio". Treat it as a lo-fi effect, not a mute. For musical muting and unmuting, send a gate or a trigger instead.

## Right-click menu

- **Panel**: follow Rack's dark-panels setting (default), or force the silver or the black panel. The choice is saved with the patch.

## Installing

Mult is free. Open the VCV Library, find Mult by Ormer Modular, and subscribe. It appears in Rack's module browser the next time Rack starts. It needs VCV Rack 2, the Free or the Pro edition, on Windows, macOS (Intel or Apple silicon) or Linux.

## Troubleshooting

**Nothing comes out of an output.** Check its chance knob: at 0% it never passes. Check that the input rises past 0.1 V and falls back to 0 V or below, and that a hit has happened since the patch loaded. Until the first hit all outputs sit at 0 V.

**An output stays open, or stays closed, for a long time.** Outputs hold their choice until the next hit. If the input never falls back to 0 V, there is no next hit.

**Audio crackles when I turn a chance down.** That is how Mult treats audio: below 100% it drops random waveform cycles. Use gates or triggers for musical muting.

**Two outputs do not match.** That is by design. Every output makes its own choice on every hit.

**The panel colour is not what I expected.** Mult follows Rack's dark-panels setting. Force either panel from the right-click menu.

## Specifications

| | |
|---|---|
| Width | 2 HP |
| Version | 2.0.0 |
| Format | VCV Rack 2 plugin, free, closed source |
| Input | 1, polyphonic (up to 16 channels) |
| Outputs | 4, each with the input's channel count |
| Chance | 0 to 100 per cent in whole per cent steps, default 100%, one knob per output |
| Hit | input rises past 0.1 V; re-arms at 0 V or below |
| Random choices | fresh on every hit, for every output and every channel; no seeds |
| Signal path | passed unchanged: no gain, no smoothing, no added delay |
| Lights | 4, one per output, a flash of about 60 ms on a passing hit |
| Sample rates | any |
