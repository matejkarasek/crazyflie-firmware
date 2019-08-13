---
title: Development for STM32
page_id: starting_development 
---

This page aims at documenting how to start developing with Crazyflie.
This document should work for the Crazyflie 2.X.


## STM32

These instructions cover Linux systems as well as Windows when running a Ubuntu WSL Bash.

Clone the crazyflie-firmware project, or update it using the virtual
machine \"Update all projects\" script. For Crazyflie 2.X make sure the current branch is \"**master**.\"

    ~$ cd projects/crazyflie-firmware/
    crazyflie-firmware$ git checkout master   

Then make the firmware.

For **Crazyflie 2.X**:

```
crazyflie-firmware$ make PLATFORM=cf2
(...)
  DFUse cf2.dfu
Crazyflie 2.0 build!
Build 00:00000000 (20XX.XX.X-XX) CLEAN
Version extracted from git
Crazyloader build!
   text    data     bss     dec     hex filename
  XXXXX    XXXX   XXXXX  XXXXXX   XXXXX cf2.elf
rm version.c
```

### Flashing instructions Linux

To program using the radio bootloader, first install the cflib and cfclient, and put the CF2.X in bootloader mode:


For **Crazyflie 2.X**:
```
    crazyflie-firmware$ make cload
```

From command line the flash make target flashed the firmware using
programming cable
```
    crazyflie-firmware$ make flash
```



#### Command line
From command line the flash make target flashed the firmware using
programming cable

    make flash

### Flashing instructions Windows 10 (Version 1903 and higher)
While you can build firmware within the Ubuntu WSL, for now, Windows Subsystem for Linux cannot access libusb devices. 
Thus, flashing needs to be done from Windows 10 via cfloader (OTA with Crazyradio PA) or using the debugger.

#### Flashing with cfloader & Crazyradio PA
To use cfloader, you need to install the CF python clients *in Windows* following these instructions:
https://github.com/bitcraze/crazyflie-clients-python/blob/master/README.md#windows-7810

Now you should be able to run cfloader from the Windows Power Shell.

To flash the firmware, you first need to launch Windows Power Shell and go to the crazyflie-firmware folder of your Ubuntu WSL (this wont work from the Command Prompt, you need to use the Windows Power Shell):
```
    cd \\wsl$\Ubuntu
    cd home\[username]\[path_to_crazyflie_projects]\crazyflie-firmware
```

Finally, you can flash the firmware by putting your Crazyflie into bootloader mode and running
```
cfloader flash cflie.bin stm32-fw
```
#### Flashing with debugger
[to be added]


