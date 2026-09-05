
This project is a fork of the [PicoDMG fork by dodger_one](https://github.com/dodger-one/PicoDMG), which in turn is a fork of [RP2040-GB for Pico-GB by YouMakeTech](https://github.com/YouMakeTech/Pico-GB), ultimately based on the Peanut-GB emulator.

The goal of this fork is to provide the firmware for 'Game Brick', a device to fit within the LEGO(R) set 72046. The hardware combines a Raspberry Pi Pico 2, an SPI MicroSD card reader, ST7789 2.8" 320x240 LCD (SPI-driven), a MAX98357 audio amplifier with 8 ohm speaker, and a custom button panel. Pin assignments for these modules are the same as for PicoDMG and Pico-GB. PCB design is in the prototype stage. The firmware will always remain open-source and full license/legal disclaimer is explained in the code.

Limitations: as a low-cost project, this device will not directly compete with the existing solutions on the market. Emulation is only for playing original Game Boy (.gb) ROMs (not Game Boy Color or Game Boy Advance).There are fewer hardware features compared to the others (no headphone socket, no volume/contrast knobs) and a compromise in display quality (for scrolling and movement) as a result of the non-integer scaling. There are also simplifications in the LEGO(R) build to accomodate the device; the display bezel must be replaced with a 3D-printed part, instead of fitting into or behind the brick-built display window. The power is supplied from 2x AA cells, rather than a rechargeable lithium battery.

Note that this project is not endorsed by the LEGO Company, owners of the registered trademark LEGO(R), nor is it licensed by Nintendo Co., Ltd. and no game ROMs are included with this project.

## What This Fork Focuses On

- RP2350 support only (can likely still be compiled for RP2040 but that will not be the focus)
- SD card file browser with clearer text/selection and tolerance for long file names
- Display right-align to suit the Game Brick device
- Automatic colour palette re-enabled (applies colour palette based on game header)
- (not added yet) Battery low voltage indication by illuminating the unused LCD area on the left
- (not added yet) Select+B (or similar combination) to turn display scaling off
  (when scaling is on, the 160x144 Game Boy display is scaled up to 266x240, which doubles some pixels and not others)

## Current Status

Unwanted pixels/lines to the left of the emulator display have been removed.

The performance improvements of PicoDMG (thank you, dodger_one!) are working successfully.
The loading screen (animation) is temporarily disabled, as this seems to interfere with SD card file loading.
The NFC code is still present for now, but it is intended to remove this, as the Game Brick will not use NFC to identify cartridge presence.


Work in progress is:
- optimise the automatic selection of colour palettes (a lengthy, continuing process)
- monitor the VSYS supply voltage and display a red rectangle, to the left of the display area
- modify existing button-polling to add the display scaling toggle on/off
- reinstate a loading screen


## Quick Start

[RP2040_GB.uf2](https://github.com/1980alexGS/GameBrick/blob/master/build_pico2/src/RP2040_GB.uf2) is a compiled .uf2 that can be uploaded to the Pico 2 (RP2350) (assuming it is configured with the other devices connected as shown below in this file).

To recompile the project after you make changes, it is necessary to install the Raspberry Pi Pico SDK, e.g. by adding the extension to VSCode. In VSCode it is also necessary, after cloning the repository or opening the unzipped folder, to import the project into the Raspberry Pi Pico extension (by clicking Import Project).

Compiling requires two Terminal commands, the same as documented for PicoDMG - one to set up (with optional build flags);
```bash
cmake -S . -B build_pico2 -G Ninja -DPICO_BOARD=pico2 -DDISPLAY_DRIVER=ST7789
````
And the other to (re)compile, which places a .uf2 executable file in the build_pico2\src\ folder:
```bash
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

Up = GP2, 
Down = GP3, 
Left = GP4, 
Right = GP5, 
A = GP6, 
B = GP7, 
Select = GP8, 
Start = GP9

SD MISO = GP12, 
SD CS = GP13, 
SD CLK or SCK = GP14, 
SD MOSI = GP15

LCD CS = GP17, 
LCD CLK or SCL = GP18, 
LCD SDI or SDA = GP19, 
LCD RS or DC = GP20, 
LCD RST = GP21, 
LCD LED or BL = GP22, 

MAX98357A DIN = GP26, 
MAX98357A BCLK = GP27, 
MAX98357A LRC = GP28


## Credits

This project builds on prior work from:

- [PicoDMG by dodger-one](https://github.com/dodger-one/PicoDMG)
- [Pico-GB / RP2040-GB by YouMakeTech](https://github.com/YouMakeTech/Pico-GB)
- [Peanut-GB](https://github.com/deltabeard/Peanut-GB)

## Original Upstream README

The preserved historical README from dodger-one is available at [README.md](https://github.com/dodger-one/PicoDMG/blob/master/README.md).

