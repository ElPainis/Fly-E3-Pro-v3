# ⚠️⚙️ 3D-printer workshop ⚙️⚠️

This branch contains the hardware conversion guide & Klipper configuration for the **Sovol SV06 Fly-E3-Pro-v3** based on Bassamanators branch.

| Printer                                                         | Branch                                                                                    |
| --------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| Sovol SV06 |                       |
| Sovol SV06 Skr-Mini-E3-V3.0                                     | [skr-mini-e3-v3](https://github.com/bassamanator/Sovol-SV06-firmware/tree/skr-mini-e3-v3) |
| ${\normalsize{\textcolor{darkturquoise}{\texttt{Sovol SV06 Fly-E3-Pro-v3}}}}$                                        | ⚡ ${\small{\textcolor{darkturquoise}{\texttt{YOU ARE HERE}}}}$ ⚡   |
| Sovol SV06 Plus                                                 | [sv06-plus](https://github.com/bassamanator/Sovol-SV06-firmware/tree/sv06-plus)           |
| All other printers                                              | [any-printer](https://github.com/bassamanator/Sovol-SV06-firmware/tree/any-printer)       |

I am creating these files for my personal use and cannot be held responsible for what it might do to your printer. Use at your own risk.

## Outline
- [Contribution](#contribution)
- [Preface](#preface)
- [Disclaimer](#Disclaimer)
- [Features](#features)
- [Stay Up-to-Date](#stay-up-to-date)
- [Hardware Conversion](#Hardware Conversion)
 - [BOM](#BOM)
 - [Electrical wireing](#electrical-wireing)
 - [Modifing Extruder Ribbon-Cable](#Modifing-Extruder-ribbon-Cable)
 - [Modifing Mobo enclosure](#Modifing-Mobo-enclosure)
 - [Wireing Steppers](#wireing-steppers)
- [Preface](#preface)
- [Before You Begin](#before-you-begin)
- [Klipper Installation](#klipper-installation)
  - [Flash Firmware](#flash-firmware)
  - [Download OSS Klipper Configuration](#download-oss-klipper-configuration)
- [Initial Steps](#initial-steps)
  1. [Adjust Configuration with MCU Path](#adjust-configuration-with-mcu-path)
  2. [Configure Your Printer](#configure-your-printer)
- [Adjust Your Slicer](#adjust-your-slicer)
- [Support Me](#support-me)
- [Directory Structure](#directory-structure)
- [FAQ](#faq)
- [Useful Resources](#useful-resources)
- [Sovol Official Links](#sovol-official-links)
- [Sources](#sources)

## Contribution
I want to thank Bassamanator for sharing his Klipperconfig, Jan Oerter and Dominik Schmidt for their Anycubic i3 Mega conversion that inspired me. Check Out [their GitHub](https://github.com/Schmelzerboy/I3-Mega-Klipper&ved=2ahUKEwj_2fKx-8qEAxW__7sIHc9iDd8QFnoECBUQAQ&usg=AOvVaw2BVSSPE56Auy_gCTLLL8iX) as well. And I thank the big maker-Community in general for advice and sharing all of your creation without this whole project wouldnt be possible. Youre breathtaking!

## Preface
💎
This Mod includes manipulation of the hardware. If this mod doesnt work out for you its in majority reversable. You have to live with some minor cosmetic changes of the machine.

🪛
This Mod needs crimping and solder tools as well as a minimum of skills with these. So I assume you have these and the basic skills to use them. I will provide as many as helpful sources as I can to make it as easy as possible to handle the provided guide. So if youre a beginner I will try my very best to hold your hand while doing this conversion. But keep in mind youre the only one that can be hold responsible if things go wrong.

Tools needed:
- Soldering iron & flux
- Crimptool for insulated Terminals
- Shrink Tubes
- Dupon Connectors
- Heatgun
- Pliers to cut and to Grab
- wire stripper

🐕‍🦺
Even though I tried to make everything as easy as possible the prequesition is also youre familiar with Klipper. Over all I would recommend this Mod to advanced klipper-users which means you have at least used and modified Klipper once and understand most part of it.

## DISCLAIMER:
The conversion needs modification of the PSU wireing. There is the potential risk of frying components, damaging your machine, firehazard or worst threading your life when doing wrong. If you unshure how to do proceed stop and get help. Dont improvise at something that can potentialy threading your life when improper! Also please leave feedback and open an issue so this guide can be optimized. Read the complete guide with attention. I can not be hold accountable for any damage or injuries. Youre doing this at your own risk.

🚨 Basic safety rules for electrical DIY 🚨:
- 1. Turn Off the machine and unplug the Power
- 2. Make shure it cant be plugged in or turned on again accidantial.
- 3. Don't be lazy but smart. Unplug and disassemble the parts you want to modify as far as possible to get them on a table.
- 4. Use proper tools.

## Features

- 💥 This Klipper configuration is an _endpoint_, meaning that it contains **everything** that you could possibly need in order to have an excellent Klipper experience! 💥
- Optional Neopixel for your printhead 🔴🟢🔵
- Minimum configuration settings for `Mainsail` and `Fluidd`.
- Macros:
  - **Improved** mechanical gantry calibration/`G34` macro that provides the user audio feedback, and time to check the calibration.
  - Z-Tilt to further improve parallel alignment to printbed. 
  - Misc macros: `PRINT_START`, `CANCEL_PRINT`, `PRINT_END`, `PAUSE`, `RESUME`.
  - Parking macros (parks the printhead at various locations): `PARKFRONT`, `PARKFRONTLOW`, `PARKREAR`, `PARKCENTER`, `PARKBED`.
  - Load/unload filament macros.
  - `PURGE_LINE` macro.
  - `TEST_SPEED` macro. Find instructions [here](#how-do-i-use-the-test_speed-macro).
- Klipper Adaptive Meshing & Purging (KAMP) integrated. Read about it [here](#how-do-i-enable-kamp-klipper-adaptive-meshing--purging).

[🔼 Back to top](#outline)

## Stay Up-to-Date

${\normalsize{\textcolor{goldenrod}{\texttt{Star ⭐ this project.}}}}$

Watch for [updates](https://github.com/bassamanator/Sovol-SV06-firmware/discussions/37).

<img src="./images/githubstar.gif" width="500" alt='github star'/>

[🔼 Back to top](#outline)

## Hardware Conversion
## BOM
| Kind  | Part | Price | Source |
| ----- | ---- | ----- | ------ |
| Electronics  | Fly-E3-Pro-V3 | ~40 Money  | [AliExpress](https://a.aliexpress.com/_EwY8p5L) |
| Wireing  | 200cm each AWG14 Red & Black  | ~4 Money  | [AliExpress](https://a.aliexpress.com/_ExgydLn)  |

[🔼 Back to top](#outline)

## Before You Begin

- This entire page is a **9 minute read**. Save yourself _hours of troubleshooting_ and read this documentation fully.
- ⚠️ Make sure your printer is in good physical condition, because print and travel speeds will be _a lot faster_. Beginners would be wise to run through [these steps](https://github.com/bassamanator/everything-sovol-sv06/blob/main/initialsteps.md).
- ⚠️ [Disable](https://github.com/bassamanator/everything-sovol-sv06/blob/main/howto.md#disable-usb-cable-5v-pin) the USB cable's 5V pin.
- Follow the steps in order. If an error was reported at a step, do no proceed to the next step.
- It is assumed that you are connected to your host Raspberry Pi (or other host device) via SSH, and that your printer motherboard is connected to the host via a data USB cable. 💡 Most of the micro USB cables that you find at home are _unlikely_ to be data cables, and it is not possible to tell just by looking.
- It is also assumed that the username on the host device is `pi`. If that is not the case, edit `moonraker.conf` and `cfgs/misc-macros.cfg` to change any mentions of `/home/pi` to `/home/yourUserName`.
- Klipper _must_ be installed on the host beforehand. Easiest is to use [MainsailOS](https://github.com/mainsail-crew/mainsail/releases/latest). [KIAUH](https://github.com/th33xitus/kiauh) is another option.
- Klipper _must_ be up to date.
  - In `Fluidd`, you can do this from `Settings` > `Software Updates`.
  - In `Mainsail`, you can do this from `Machine` > `Update Manager`.
- Robert Redford's performance in _Spy Game (2001)_ was superb!
- It is assumed that there is one instance of Klipper installed. If that is not the case, the steps in this guide will not work _perfectly_ for you.
- Your question has probably been answered already, but if it hasn't, please post in the [Discussion](https://github.com/bassamanator/Sovol-SV06-firmware/discussions) section.
- I would recommend searching for the word `NOTE` in this configuration. There are roughly half a dozen short points amongst the various files that you should be aware of.
<!-- - Link to recommended parts. -->

[🔼 Back to top](#outline)

## Klipper Installation

### Flash Firmware

💡 If you flashed Klipper onto your motherboard in the past, you can skip this step.

Please note:

- For the sake of simplicity, I will refer to the firmware file as `klipper.bin` even though the actual filename is something along the lines of `klipper-v0.11.0-148-g52f4e20c.bin`.
- The firmware file is located in the `misc` folder.
- Flashing will only work if current firmware filename is _different from previous flashing procedure_. The `.bin` is also important.
- You may find this [video](https://youtu.be/p6l253OJa34) useful.
- ⚠️ Many users have reported having issues flashing Klipper using the Sovol microSD card.

#### 1. Prepare the microSD Card for Flashing with These Parameters

- Size: `16GB` maximum.
- File system: `FAT32`.
- Allocation unit size: `4096 bytes`.
- Must not contain any files _except_ the firmware file.

#### 2. Flashing Procedure

1. Disconnect any USB cables that might be connected to the motherboard.
2. Copy `klipper.bin` to the microSD card.
3. Make sure the printer is off.
4. Insert the microSD card into printer.
5. Turn on the printer and wait a minute (usually takes 10 seconds).
6. Turn off the printer and remove the microSD.

⏲️ At this point, it's not possible to tell with certainty whether your flash was successful, continue on with the guide.

[🔼 Back to top](#outline)

### Download OSS Klipper Configuration

#### Method 1: Clone the Repository

💡 Make sure `git` is installed (`sudo apt update && sudo apt install git`).

1. `cd ~/printer_data/config`
2. Empty entire `~/printer_data/config` folder.
   - In linux, you can delete files via `rm fileName` and directories via `rmdir directoryName`.
   - In linux, you can list files and folders via `ls -lah`.
3. `git clone -b master --single-branch https://github.com/bassamanator/Sovol-SV06-firmware.git .` ⚠️ Don't miss the period!

#### Method 2: Download the ZIP

1. [Download](https://github.com/bassamanator/Sovol-SV06-firmware/archive/refs/heads/master.zip) the `ZIP` file containing the Klipper configuration.
2. See `Step 2` in `Method 1`.
3. The parent folder in the `ZIP` is `Sovol-SV06-firmware-master`. This is relevant in the next step.
4. Extract **only** the _contents_ of the parent folder into `~/printer_data/config`.

[🔼 Back to top](#outline)

## Initial Steps

### Adjust Configuration with MCU Path

💡 Make sure the host and printer are connected via USB.

1. Find what port the `mcu` (printer motherboard) is connected to via _one_ of the following commands:

   - `ls /dev/serial/by-id/*`
   - `ls /dev/serial/by-path/*`

   1. The output will be something along the lines of
      - `/dev/serial/by-id/usb-1a86_USB2.0-Serial-if00-port0`

2. Adjust the `[mcu]` section in `printer.cfg` accordingly.

   ```yaml
   # 📝 This is just an example
   [mcu]
   serial: /dev/serial/by-id/usb-1a86_USB2.0-Serial-if00-port0
   restart_method: command
   ```

3. Do a `FIRMWARE_RESTART`.

If the Klipper flash that you did earlier was successful, and you've done everything else correctly, you should see no errors or warnings in the `Mainsail`/`Fluidd` dashboard. 🎉 **Your printer has been Klipperized!** 🎉

[🔼 Back to top](#outline)

### Configure Your Printer

❗☠️ **Your finger should be on the power switch for most of these steps** ☠️❗

❗☠️ **Power off if there is a collision/problem** ☠️❗

💡 The ${\small{\textcolor{red}{\texttt{EMERGENCY STOP}}}}$ button in your dashboard works faster than hitting the power switch.

💡 Do a practice emergency stop.

💡 I recommend no filament be loaded for any of these steps.

📝 You will be pasting/typing these commands into the `Mainsail`/`Fluidd` console.

1. Check to see if `X` and `Y` max positions can be reached, and adjust `position_max`, if necessary. You might be able to go further, which is great, but I recommend leaving a 2mm gap for safety.
   1. `G28`
   2. `G90`
   3. `G1 X223 F3000`
   4. `G1 Y223 F3000`
2. Do a mechanical gantry calibration; `G34`. After the controlled collision against the beam at the top, there will be a 10 second pause for you to verify that both sides of the gantry are pressed up against the `stoppers` at the top. You will hear a succession of beeps.
   1. Figure out your `Z` `position_max` by baby stepping your way up to the beam, and adjust `position_max`, if necessary.
3. PID tune the bed. Ideally, all PID tuning should occur at the temperatures that you print most at.
   1. `PID_TEST_BED TEMP=70`
   2. `SAVE_CONFIG` (once completed)
4. PID tune the extruder while part cooling fan runs at 25%.
   1. `PID_TEST_HOTEND TEMP=245`
   2. `SAVE_CONFIG` (once completed)
5. Adjust `z_offset`. Make sure your nozzle if very clean. Do the [Paper test](https://www.klipper3d.org/Bed_Level.html?h=probe_calibrate#the-paper-test).
   1. `DO_PROBE_CALIBRATE`
   2. Follow `z_offset` setup in `Mainsail`/`Fluidd`.
   3. `SAVE_CONFIG` (once completed)
6. Create a bed mesh.
   1. `DO_CREATE_MESH`
   2. `SAVE_CONFIG` (once completed)

🏁 If you've made it here, then your Klipperized printer is ready to print! 🏁

_But first_, adjust your slicer.

[🔼 Back to top](#outline)

## Adjust Your Slicer

📝 If you are using the slicer bundles found on this repo, you can skip this section.

### Start G-Code

It varies depending on your slicer. Find instructions [here](https://ellis3dp.com/Print-Tuning-Guide/articles/passing_slicer_variables.html#slicer-start-g-code).

### End G-Code

```
PRINT_END
```

### Line Purge

If you would like to print a purge line before your print starts, at the end of your start gcode, on a new line, add one of the following:

- `PURGE_LINE`; prints a standard purge line.
- `LINE_PURGE`; prints KAMP's purge line. ⚠️ Do not attempt to use without reading [this section](#how-do-i-enable-kamp-klipper-adaptive-meshing--purging).

```yaml
# 📝 This is just an example Start G-Code
PRINT_START ...
PURGE_LINE
```

[🔼 Back to top](#outline)

## Support Me

Please ⭐ star this repository!

Support [open source](https://en.wikipedia.org/wiki/Open_source), and buy me a [<img src="./images/logo_white_stroke.png" height="20" alt='Ko-fi'/>](https://ko-fi.com/bassamanator).

[🔼 Back to top](#outline)

## Directory Structure

This repository contains many files and folders. Some are _necessary_ for this Klipper configuration to work, others are not.

- **Necessary** items are marked with a ✅.
- Items that can _optionally_ be deleted are marked with a 💠.
<!-- tree -a -C -I '.directory' -L 1 -F -->

```sh
├── cfgs/ ✅
├── CODE_OF_CONDUCT.md 💠
├── CONTRIBUTING.md 💠
├── .git/ ✅❔
├── .github/ 💠
├── .gitignore ✅❔
├── images/ 💠
├── LICENSE 💠
├── misc/ 💠
├── moonraker.conf ✅
├── osskc.cfg ✅
├── printer.cfg ✅
├── README.md 💠
├── SECURITY.md 💠
└── .vscode/ 💠
```

[🔼 Back to top](#outline)

## FAQ

### What are some settings that I can change?

Edit the relevant file according to your needs.

| File                   | Section                  |
| ---------------------- | ------------------------ |
| `cfgs/misc-macros.cfg` | `[gcode_macro _globals]` |

| Variable                           | Disable       | Enable        | Notes                                                               |
| ---------------------------------- | ------------- | ------------- | ------------------------------------------------------------------- |
| `variable_beeping_enabled`         | `0`           | `1` (default) |
| `variable_filament_sensor_enabled` | `0` (default) | `1`           |
| `variable_kamp_enable`             | `0` (default) | `1`           | See [here](#how-do-i-enable-kamp-klipper-adaptive-meshing--purging) |

### How do I import a configuration bundle into SuperSlicer/PrusaSlicer?

Please see this [discussion](https://github.com/bassamanator/Sovol-SV06-firmware/discussions/13).

### How do I print using SuperSlicer/PrusaSlicer?

Please see this [discussion](https://github.com/bassamanator/Sovol-SV06-firmware/discussions/14).

### When does beeping occur?

The printer will beep upon:

- Filament runout.
- Filament change/`M600`.
- Upon `PRINT_END`.
- `MECHANICAL_GANTRY_CALIBRATION`/`G34`.

### I want to use a filament sensor. How do I set it up?

You can find information about the physical setup [here](https://github.com/bassamanator/everything-sovol-sv06#filament-sensor).

### My filament runout sensor works, but I just started a print without any filament loaded. What gives?

A simple runout sensor can only detect a change in state. So, if you start a print without filament loaded, the printer will not know that there is no filament loaded. You should test your sensor by having filament loaded, starting a print, then cutting the filament. The expected behaviour is that the print will pause, and as long as you have beeping enabled, you will hear 3 annoying beeps.

### What happens when I put in `M600`/colour change at a certain layer?

1. The printer will beep 3 times (not annoyingly).
2. Printing will stop.
3. The printhead will park itself front center.
4. The hotend will turn off, but the bed will remain hot.

### What happens when I pause a print?

Same behaviour as `M600`/colour change _except_ there won't be any beeping.

### What happens when filament runs out?

_If_ you have a working filament sensor, the same behaviour as `M600`/colour change will occur _except_ the beeps will be fairly annoying.

### How do I resume a print after a colour change or filament runout?

⚠️ Do not disable the stepper motors during this process!

The printhead is now parked front center waiting for you to insert filament. You will:

1. Heat up the hotend to the desired temperature.
   - Use your Klipper dashboard.
2. Purge (push) some filament through the nozzle.
   - Use your Klipper dashboard, and extrude maybe 50mm (for a colour change you probably want to extrude more).
   - OR, you can push some filament by hand _making sure to first disengage the extruder's spring loaded arm_.
3. Hit resume in your Klipper dashboard.

### How do I enable KAMP (Klipper Adaptive Meshing & Purging)?

⚠️ No KAMP functionality can be used on low-powered devices such as the Raspberry Pi Zero.

⚠️ If KAMP is disabled, and there is no `default` mesh, `PRINT_START` will crash.

📝 The [Label objects setting](https://docs.mainsail.xyz/overview/features/exclude-objects#enable-the-label-objects-setting-in-your-slicer) in your slicer must be enabled for KAMP to work.

📝 `LINE_PURGE` is useable (on appropriate devices) even if KAMP is disabled.

This repo contains all the code from the KAMP repository, however, only the `adaptive meshing` and `LINE_PURGE` functionality of KAMP has been configured and tested for use. To enable other functionality, adjust `/cfgs/kamp/KAMP_Settings.cfg`.

### How do I use the `TEST_SPEED` macro?

⚠️ This is for advanced users only, with well oiled machines. You can cause serious damage to your printer if you're not careful. ☠️ **You have been warned** ☠️.

Find full instructions [here](https://ellis3dp.com/Print-Tuning-Guide/articles/determining_max_speeds_accels.html).

Some tips:

- Before running with `ITERATIONS=40` with an untested speed/accel value, run with `ITERATIONS=1`.
- Pay close attention throughout the run, so that you can click ${\small{\textcolor{red}{\texttt{EMERGENCY STOP}}}}$ at a moment's notice.
- This macro will simply help you determine the maximum speed your printhead and bed can reliably move at, not necessarily print at. The bottleneck for my SV06, for example, is the 15mm/s^2 that the hotend maxes out at (well under 200mm/s actual print speed).

### How do I compile my own firmware?

Please see this [discussion](https://github.com/bassamanator/Sovol-SV06-firmware/discussions/111).

[🔼 Back to top](#outline)

## Useful Resources

- [Everything Sovol SV06](https://github.com/bassamanator/everything-sovol-sv06)
- [RP2040-Zero ADXL345 Connection Klipper](https://github.com/bassamanator/rp2040-zero-adxl345-klipper)
- ⭐⭐⭐⭐⭐ [Ellis' Print Tuning Guide](https://ellis3dp.com/Print-Tuning-Guide)
- [Simplify3D Print Quality Troubleshooting Guide](https://www.simplify3d.com/resources/print-quality-troubleshooting/
-https://support.th3dstudio.com/helpcenter/ezboard-v2-sovol-sv06-stock-abl-sensor-wiring/
-https://sv06.blakadder.com/Parts/electronic-parts/
-https://teamgloomy.github.io/fly_e3_pro_v3_general.html

[🔼 Back to top](#outline)

## Sovol Official Links

- [SV06 Marlin Source Code](https://github.com/Sovol3d/Sv06-Source-Code)
- [SV06 Models](https://github.com/Sovol3d/SV06-Fully-Open-Source)
- [SV06 Plus Marlin Source Code and Models](https://github.com/Sovol3d/SV06-PLUS)

[🔼 Back to top](#outline)

## Sources

- [https://www.klipper3d.org](https://www.klipper3d.org)
- [Ellis' Print Tuning Guide](https://ellis3dp.com/Print-Tuning-Guide)
- [Mechanical Gantry Calibration Macro](https://github.com/strayr/strayr-k-macros)
- [SV06 printer.cfg](https://github.com/spinixguy/Sovol-SV06-firmware)
- [SV06 Buildplate and Texture](https://www.printables.com/model/378915-sovol-sv06-buildplate-texture-and-model-for-prusas)
- [Ellis' SuperSlicer Profiles](https://github.com/AndrewEllis93/Ellis-SuperSlicer-Profiles)
- [Klipper Adaptive Meshing & Purging](https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging)
- [PrusaSlicer Print Settings](https://github.com/mjonuschat/PrusaSlicer-Profiles)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/H2H0HIHTH)

[🔼 Back to top](#outline)
