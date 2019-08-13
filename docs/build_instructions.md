---
title: Building Crazyflie 2.0 firmware
page_id: build_instructions
---

## Dependencies

You'll need to use either the [Crazyflie VM](https://wiki.bitcraze.io/projects:virtualmachine:index),
[the toolbelt](https://wiki.bitcraze.io/projects:dockerbuilderimage:index) or 
install some ARM toolchain.

### Install a toolchain

#### OS X
```bash
brew tap PX4/homebrew-px4
brew install gcc-arm-none-eabi
```

#### Debian/Ubuntu

Tested on Ubuntu 14.04 64b, Ubuntu 16.04 64b, and Ubuntu 18.04 64b:

For Ubuntu 14.04 :

```bash
sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded
sudo apt-get update
sudo apt-get install libnewlib-arm-none-eabi
```

For Ubuntu 16.04 and Ubuntu 18.04:

```bash
sudo add-apt-repository ppa:team-gcc-arm-embedded/ppa
sudo apt-get update
sudo apt install gcc-arm-embedded
```

Note: Do not use the `gcc-arm-none-eabi` package that is part of the Ubuntu repository as this is outdated.

#### Arch Linux

```bash
sudo pacman -S community/arm-none-eabi-gcc community/arm-none-eabi-gdb community/arm-none-eabi-newlib
```

#### Windows

In Windows 10, the firmware can be developed within the Windows Subsystem for Linux (WSL). It is recommended to update your Windows 10 to version 1903 or newer.

In Microsoft Store, install Ubuntu (this guide is written for Ubuntu 18.04).

Once installed, launch Ubuntu WSL and install git & make:

```bash
sudo apt-get update
sudo apt install git
sudo apt install make
```

Further install the toolchain as in native Ubuntu (16.04 / 18.04)
```bash
sudo add-apt-repository ppa:team-gcc-arm-embedded/ppa
sudo apt-get update
sudo apt install gcc-arm-embedded
```

### Cloning

This repository uses git submodules. Clone with the `--recursive` flag

```bash
git clone --recursive https://github.com/bitcraze/crazyflie-firmware.git
```

If you already have cloned the repo without the `--recursive` option, you need to 
get the submodules manually

```bash
cd crazyflie-firmware
git submodule init
git submodule update
```


## Compiling

### Crazyflie 2.X

This is the default build so just running ```make``` is enough or:
```bash
make PLATFORM=cf2
```

or with the toolbelt

```bash
tb make PLATFORM=cf2
```

### Roadrunner

Use the ```tag``` platform

```bash
make PLATFORM=tag
```

or with the toolbelt

```bash
tb make PLATFORM=tag
```


### config.mk
To create custom build options create a file called `config.mk` in the `tools/make/`
folder and fill it with options. E.g. 
```
PLATFORM=CF2
DEBUG=1
CLOAD=0
```
More information can be found on the 
[Bitcraze wiki](http://wiki.bitcraze.io/projects:crazyflie2:index)

# Make targets:
```
all        : Shortcut for build
compile    : Compile cflie.hex. WARNING: Do NOT update version.c
build      : Update version.c and compile cflie.elf/hex
clean_o    : Clean only the Objects files, keep the executables (ie .elf, .hex)
clean      : Clean every compiled files
mrproper   : Clean every compiled files and the classical editors backup files

cload      : If the crazyflie-clients-python is placed on the same directory level and 
             the Crazyradio/Crazyradio PA is inserted it will try to flash the firmware 
             using the wireless bootloader.
flash      : Flash .elf using OpenOCD
halt       : Halt the target using OpenOCD
reset      : Reset the target using OpenOCD
openocd    : Launch OpenOCD
```

