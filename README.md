This project is a fork of the [PicoDMG fork by dodger_one](https://github.com/dodger-one/PicoDMG), which in turn is a fork of [RP2040-GB for Pico-GB by YouMakeTech](https://github.com/YouMakeTech/Pico-GB), ultimately based on the Peanut-GB emulator.

The goal of this fork is to provide the firmware for 'Game Brick', a device to fit within the LEGO(R) set 72046.
The hardware combines a Raspberry Pi Pico 2, an SPI MicroSD card reader, ST7789 2.8" 320x240 LCD (SPI-driven), a MAX98357 audio amplifier with 8 ohm speaker, and a custom button panel. Pin assignments for these modules are the same as for PicoDMG and Pico-GB.

PCB design is in the prototype stage. PCBs or completed devices may be sold in the future, but no earlier than November 2026.
As a low-cost project, this device will not directly compete with the existing solutions on the market, as the feature set is limited to only original Game Boy DMG emulation, there are fewer hardware features (no headphone socket, no volume/contrast knobs) and a compromise in display accuracy (for scrolling and movement) as a result of the non-integer scaling. There are also simplifications in the LEGO(R) build to accomodate the device; the display bezel must be replaced with a 3D-printed part, instead of fitting into or behind the brick-built display window. The power is supplied from 2x AA cells, rather than a rechargeable lithium battery.

Note that the project is not endorsed by the LEGO Company, owners of the registered trademark LEGO(R).

## What This Fork Focuses On

- RP2350 support only (can likely still be compiled for RP2040 but that will not be the focus)
- SD card file browser with clearer text/selection and tolerance for long file names
- Display right-align to suit the Game Brick device
- Automatic colour palette re-enabled (applies colour palette based on game header)
- (not added yet) Battery low voltage indication by illuminating the unused LCD area on the left
- (not added yet) Select+B (or similar combination) to turn display scaling off
  (when scaling is on, the 160x144 Game Boy display is scaled up to 266x240, which doubles some pixels and not others)

## Current Status

The performance improvements of PicoDMG (thank you, dodger_one!) are working successfully.
The loading screen (animation) is temporarily disabled as this currently interferes with file loading.
The NFC code is still present for now, but it is intended to remove this, as the Game Brick will not use NFC to identify cartridge presence.
Some colour palette automatic selections have been adjusted.

Work in progress is:
- prevent the unwanted display of pixel lines to the left of the display area
- monitor the VSYS supply voltage and display a red rectangle, to the left of the display area
- modify existing button-polling to add the display scaling toggle on/off
- reinstate a loading screen


## (no) Quick Start (yet!)

At the moment, the only way to explore this project is to compile the source code (there is no precompiled .uf2 yet)
It is necessary to install the Raspberry Pi Pico SDK (e.g. by adding the extension to VSCode)
Compiling requires two Terminal commands, the same as documented for PicoDMG;
```bash
cmake -S . -B build_pico2 -G Ninja -DPICO_BOARD=pico2 -DDISPLAY_DRIVER=ST7789
cmake --build build_pico2 -j --target RP2040_GB
```
Note; the target is RP2040_GB even when compiling for the Pico2.


## Hardware At A Glance

The current build/documentation assumes combinations of:

- Raspberry Pi Pico 2 (RP2350)
- 2.8" SPI TFT display (ST7789)
- microSD storage for ROMs
- MAX98357A for audio
- D-pad and A/B, Start and Select buttons wired as for YouMakeTech's Pico-GB:

Up = GPIO2
Down = GPIO3
Left = GPIO4
Right = GPIO5
A = GPIO6
B = GPIO7
Select = GPIO8
Start = GPIO9

SD MISO = GPIO12
SD CS = GPIO13
SD CSK = GPIO14
SD MOSI = GPIO15

LCD CS = GPIO17
LCD CLK = GPIO18
LCD SDI = GPIO19
LCD RS = GPIO20
LCD RST = GPIO21
LCD LED = GPIO22

MAX98357A DIN = GPIO26
MAX98357A BCLK = GPIO27
MAX98357A LRC = GPIO28


## Credits

This project builds on prior work from:

- [PicoDMG by dodger-one](https://github.com/dodger-one/PicoDMG)
- [Pico-GB / RP2040-GB by YouMakeTech](https://github.com/YouMakeTech/Pico-GB)
- [Peanut-GB](https://github.com/deltabeard/Peanut-GB)

## Original Upstream README

The preserved historical README from dodger-one is available at [README.md](https://github.com/dodger-one/PicoDMG/blob/master/README.md).

