# Xiaomi NoteBook Pro tweaks

Many BIOS-level tweaks to improve this great laptop

[English](README.md) | [Rus](README-RU.md)

## Features

* Custom fan curve to fix constant fan noise
* Charge fix for 603 BIOS + external hub
* Undervolting feature enable for latest 502 and 603 BIOS
* Custom TDP configuration set
* SpeedShift technology enable
* for MacOS users: DVMT custom size set
* for MacOS users: 0xE2 Lock disable

## Plans

* Configurable keyboard backlit

## Credits

- [PavelLJ](https://github.com/PavelLJ) for his help
- [saltukkos](https://github.com/saltukkos) for GUI tool to make your own fan curve

## Installation
Your BIOS version should be XMAKB5R0P0603! Update if necessary. The default version is +12°, if you need the version +20°, replace ec604.bin with the corresponding one from the /EC folder. If you need to be able to charge the laptop through the hub, use the /EC502 folder. If you want to create your own profile, take the original EC file from the EC/Orig or EC502/Orig folder and edit using https://github.com/saltukkos/xiaomi-notebook-pro-bios-patcher/releases

0. Make a full dump of your BIOS firmware: backup.cmd, save file mybackup.bin outside of laptop 
1. Remove write protection BIOS: bios_unlock.cmd, be sure to reboot
2. Save your EC: readEC.cmd, the ec.bin file will appear, this is your EC backup
3. Flash new EC: flashEC.cmd, will be flashed ec604.bin
4. First pull out the power cable, then completely turn off the laptop (Start->Shutdown, not just close the lid), wait a minute, insert the cable, wait 5 seconds, turn on the laptop
5. Put back write protection for BIOS: bios_lock.cmd

## Possible errors and how to fix them
1. The firmware dump utility reports:
Error 318: The host CPU does not have read access to the target flash area. To enable read access for this operation you must modify the descriptor settings to give host access to this region. FPT Operation Failed.
 - it is necessary at least once to start BIOS update procedure, until the "unlockme" step inclusive, after that the procedure can be interrupted

2. Problems with security policies and the inability to run PowerShell scripts, for example:
"The .\Patchscript_bue.ps1 file does not have a digital signature. The script can not be run bla bla bla"
 - enter the following from the command line: powershell set-executionpolicy remotesigned
 - in group security policies, you must enable scripting for powershell

3. Coolers after the patch are still kicked at 42°
 - check that the firmware update was successful: run again readEC.cmd, compare new ec.bin and ec604.bin, now they should be binary same
 - Repeat step number 4, sometimes you need to juggle the cable several times (almost always more than one)
 - disconnect the power cable, hold the power button for a long time until the laptop switches off, wait a minute, connect the cable, wait 10 seconds, switch on
 - if the firmware update was successful, but all manipulations with the power cable was unsuccessful, then it remains only to throw off the battery cable for a couple of minutes, or just wait, sooner or later the EC will read new firmware, after one of the reboots or after a night's sleep

## How to roll back
1. Flash the original BIOS 
2. Flash only the EC from backup ec.bin, by the instructions above, also the original file can be found here: EC\Orig\ec603.bin

## Install other tweaks
- Enable CPU undervolting feature: run the script voltage_unlock.cmd
- Create a custom TDP profile: edit and run the TDP_set.cmd script
- Enabling Intel SpeedShift Technology (SST): run the script speedshift_unlock.cmd
- for MacOS users: change the parameter DVMT: edit and run the script DVMT_set.cmd
- for MacOS users: 0xE2 Lock: run the script CFG_unlock.cmd
