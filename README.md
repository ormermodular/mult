<p align="center"><img src="docs/images/mult-banner.svg" alt="Mult by Ormer Modular" width="100%"></p>

<p align="center">
  <img alt="Licence: free, closed source" src="https://img.shields.io/badge/licence-free%20%C2%B7%20closed%20source-lightgrey">
  <img alt="Expert Sleepers disting NT" src="https://img.shields.io/badge/disting%20NT-firmware%201.19%2B-e2a24a">
</p>

<p align="center"><b>A chance mult: one input, four outputs, each with its own chance of passing every hit.</b></p>

Mult shares one signal out to four outputs, and every output has its own chance of passing each incoming hit. Feed it a gate or a trigger and each output tosses its own coin: one hit might reach outputs 1 and 4, the next none, the next all of them.

Turn a chance down and that output starts dropping hits, so one clock or drum pattern thins out differently across several voices. At 100% an output is a plain copy of the input, so out of the box it is just a mult. Every choice is fresh and purely random, with no seeds and no evenly spaced modes.

One screen shows four lanes, one per output: the left encoder selects a lane, the right encoder sets its chance, and pushing the right encoder sets it back to 100%. Threshold sets how far the input must rise to count as a hit.

<p align="center"><a href="https://ormermodular.github.io/mult/nt/">disting NT manual</a> · <a href="https://ormer.dev">Ormer Modular</a></p>

## Installing

Mult is free. It needs [disting NT firmware 1.19 or newer](https://www.expert-sleepers.co.uk/distingNTfirmwareupdates.html).

1. Download `mult-plugin.zip` from the latest release.
2. Unzip it at the root of the disting NT SD card.
3. Restart the module or remount the card, then add **Mult**.

The archive installs `mult.o` at `/programs/plug-ins/ormermodular/mult.o`. No compiler or development toolchain is required.

The [manual](https://ormermodular.github.io/mult/nt/) covers every control and what counts as a hit.

## Credits

Made by Ormer Modular in Guernsey.

## Licence

Mult is free to use. It is closed source: no licence is granted to copy, modify or redistribute the software or its artwork.
