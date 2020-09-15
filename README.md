# Thinkpad T430s Hackintosh with OpenCore 0.6.1
![](./Resources/cover.png)
So I think maybe this is the first OC folder for our Thinkpad T430s. I have tried several different macOS versions and premade EFIs, but in my opinion this one which I made is the most compatible one for Mojave 10.14.6, at least on my own machine.
I don't guarantee that this config will work great on your machine, so it is highly recommended to use this repository for reference only.
## My hardware specs
- CPU: Intel Core i5-3320M.
- RAM: 8 GB.
- SSD: Crucial BX500 256 GB (in main 2.5" slot).
- Orico caddy bay.
- Screen: TN 1600x900.
## Software
- OpenCore 0.6.1.
- ~~macOS Catalina 10.15.6.~~
- Works much better with macOS Mojave 10.14.6.
- Kexts: AppleALC, BrcmBluetoothInjector, BrcmPatchRAM3, IntelMausi, Lilu, WhatEverGreen, VirtualSMC, SMCBatteryManagement, SMCProcessor, SMCSuperIO, VoodooInput, VoodooPS2Controller. 
## What's working (as I have tested so far)
- Intel HD Graphics 4000 w/ QE-CI.
- Speaker, headphone jack output and intergrated microphone (``alcid=28``).
- Keyboard.
- Backlight control via ``Fn-F8/F9``.
- TrackPoint and TrackPoint buttons.
- Battery status.
- USB ports.
- Sleep.
## Not working well
- Trackpad is sluggish. I don't really know how to fix it.
## Not working
- Intergrated Wifi and Bluetooth.
- Touchpad lower buttons.
- VGA output.
- Hard disk LED (it turns on forever, no blinking, etc.).
## Not tested
- DisplayPort output (shown in Hackintool but not tested).
- Intergrated camera (it's broken on my laptop).
## Generate your own DSDT/SSDT for better compability.
- Dump and patch your own ``DSDT.aml`` as guided [here](https://www.tonymacx86.com/threads/guide-lenovo-thinkpad-t430-clover.229576/). Replace the prebuilt ``DSDT.aml`` in ``OC/ACPI`` with yours.
- Follow Dortania's guide on Ivy Bridge power management fix [here](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management). Replace the prebuilt ``SSDT-PM.aml`` in ``OC/ACPI`` with yours (the default name of the generated SSDT is ``ssdt.aml``, you'll need to rename it to ``SSDT-PM.aml``).
- Enable ``USBInjectAll.kext`` in ``config.plist`` and use Hackintool.app to generate your own ``USBPorts.kext``, ``SSDT-EC-USB.aml`` and ``SSDT-UIAC.aml`` (plenty of guides about this are available on Google). Put your ``USBPorts.kext`` to ``OC/Kexts`` and the SSDTs into ``OC/ACPI``. Finally disable ``USBInjecAll.kext`` like the way you enabled it.
- Run these commands in a terminal to for better sleeping:
```
sudo pmset -a hibernatemode 0
sudo pmset autopoweroff 0 
sudo pmset powernap 0 
sudo pmset standby 0
sudo pmset proximitywake 0
```
- If you have an extra HDD installed in your DVD slot (via a caddybay), you'll need to replace your ``AppleAHCIPort.kext`` with the older one which I provided in the Extra folder in this repo (grabbed from InsanelyMac) to have your HDD recognized in macOS.
  - Make a backup of your current ``/S/L/E/AppleAHCIPort.kext``.
  - Copy the provided kext into ``/S/L/E``. Remember to correct its permissions then finally perform a kextcache update.
  - You should put the disk on which you installed macOS in the default 2.5" slot rather than the DVD slot.
## Changelog
```
11-Sep-2020: initial build
16-Sep-2020: changed for better compability with Mojave. Catalina is not fully supported. Updated additional guides on DSDT/SSDT patching.
```
## Special thanks
- OpenCore, macOS and other tools' developer team.
- Dortania's vanilla guide.
- This DSDT patching guide for T430s: https://www.tonymacx86.com/threads/guide-lenovo-thinkpad-t430-clover.229576/

