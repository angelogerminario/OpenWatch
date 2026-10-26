# OpenWatch

**I needed a smartwatch so i tried making one, with a custom PCB, a printed case, and custom firmware, here's what i came up with.**

OpenWatch follows my earlier [Potato Watch](https://github.com/angelogerminario/Potato-watch) project. This version moves to a more serious nRF52840 (very cool chip, also used in apple airtags) and a monochrome e-paper touchscreen, with a focus on battery efficiency and features that are commonly not found on a smartwatch, like full openness of the software/hardware stack, full mifare nfc emulation and more.

> This project is still very much a work in progress. for now i have a working prototype, once testing is over i will publish everything here.

<p align="center">
  <img src="photos/On%20wrist.jpeg" alt="OpenWatch prototype on the wrist, showing the DASH watch face" width="520">
</p>

## What it does

- **Always-on e-ink display.** Readable in sunlight, with a fairly quick refresh rate. The current firmware refreshes in around 300 ms without ghosting or blinking. An experimental version reached 30 fps, but still needs refining.
- **Full MIFARE NFC support.** Mifare 1k based NFC cards can be stored on the watch for use with generic Mifare-based access control systems.
- **Onboard sensors and timekeeping.** An accelerometer and magnetometer provide motion sensing, shake detection, and a tilt-compensated compass. A dedicated RTC keeps time independently of the phone, while a fuel gauge tracks battery level and electrical measurements. Capacitive touch handles input, with vibration for alerts and feedback.
- **Bluetooth phone integration.** Sync notifications and time, see what's playing, and control media playback and volume. Currently iPhone only, using its built-in Bluetooth services without a companion app.
- **Easy to add custom apps.** A small app system makes it straightforward to implement new applications alongside the included watch faces, games, and utilities.
- **A layered OS.** Drivers feed services, and services feed apps. Each layer respects that hierarchy, keeping hardware details out of applications and making individual parts easier to edit, replace, and update.
- **Wireless firmware updates.** Load new firmware over Bluetooth using MCUboot, without opening the watch (swd interface is present but is basically only needed for first firmware flash).
- **Crash and stall recovery.** The firmware detects crashes and freezes and can automatically send the watch into update mode, allowing recovery without opening the case.
- **Unibody design.** Touch controls and wireless charging allow a case with no buttons or charging ports.
- **Qi wireless charging.** Recharge on a compatible Qi charger, with the receiver, battery charger, and protection circuitry built into the mainboard.

## Hardware

![Assembled OpenWatch PCB](photos/Pcb%20pic.jpeg)

| Part | Component | Role |
| --- | --- | --- |
| Microcontroller | u-blox BMD-340, based on the Nordic nRF52840 | Runs the watch and provides Bluetooth LE and NFC |
| Display | Good Display GDEY0154D67, 1.54-inch, 200 × 200 e-paper | Monochrome watch faces and apps |
| Touch | FT6336U | Capacitive touch input |
| Real-time clock | RV-3032-C7 | Low-power timekeeping |
| Accelerometer | BMA400 | Motion sensing and shake detection |
| Magnetometer | MMC5603NJ | Compass heading |
| Fuel gauge | BQ27441 | Battery level and electrical measurements |
| Wireless power receiver | BQ51013B | Qi charging input |
| Battery charger | BQ24072 | Battery charging and power-path management |
| Regulator | TPS63900 | Regulated supply for the watch |
| Battery protection | HY2116 with dual MOSFETs | Hardware battery protection (3.2v instead of the usual unsafe 2.6v) |


The PCB was designed in EasyEDA Pro and manufactured by JLCPCB. The board uses **0.8 mm thickness**. Schematics, manufacturing files, and the BOM are in [pcb/](pcb/); for future and more detailed remarks and manufacturing details check [PCB notes](pcb/Readme.md).

## Case

The current prototype uses a 3D-printed case around the square display and custom board. once i reach a final design i will cnc manufacture the final case in metal and add a protective custom glass with silkscreen to the display (also hiding the undesirable touch layer lines on the sides):

![OpenWatch case 3D render](photos/3d%20render%20case.png)

## Project status

There is a working wearable prototype, and both the hardware and firmware are still being refined. Battery-life figures will be added once measured.

I'll post further updates here as the project develops, followed by the full firmware source.
