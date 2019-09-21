# TBS USB drivers

These are out-of-tree modules and do not require a full v4l media tree.
Only required modules are built to add support for TBS cards in the cx231xx
module. This is only tested with ArchLinux (kernel 4.19 and 5.2).

Reasons for not using the full media build from tbsdtv are:

* The second adapter never worked on my Raspberry Pi4
* It prevents loading some Pi4 specific modules
* It takes too long to build after a kernel upgrade

There is still one issue to be resolved but that is independent of the TBS source:
USB bulk transfer of the cx231xx module causes a stalled device on the Raspberry
Pi4 kernel and it must be used with ISO transfer.

```
[/etc/modprobe.d/cx231xx.conf]
options cx231xx transfer_mode=1
```

That does not happen with an x86 kernel.

Except the general USB bulk transfer issue no further problems have been detected.
My TBS 5990 runs with both adapters for quite some time now.

This repository is heavily inspired by https://github.com/AlexanderS/tbsecp3-driver.
The upstream driver sources are located at https://github.com/tbsdtv/linux_media.

## Contents

This repos contains the following modules:

* av201x
* tas2101
* cx231xx_dvb_ci
* cx231xx

## Modification

The upstream files were only modified to fix build issues with the host
kernel. I used the official cx231xx files and added the TBS specific
changes. Some kernel version specific branches (ifdef) have been added.

The initialization functions of the usb transfers for the second adapter
have been adopted to the setup functions of the first adapter.

## Supported cards

* TBS 5280
* TBS 5281
* TBS 5990

## Build

To build the modules just execute:

```
make
```

and install the modules with:

```
make modules_install
```

This will build the modules for the running kernel. If you want to build the
modules for another kernel (maybe during update before rebooting) you can use
the `KDIR` variable:

```
make KDIR=/lib/modules/4.18.12-arch1-1-ARCH/build
make KDIR=/lib/modules/4.18.12-arch1-1-ARCH/build modules_install
```

To install them into a different directory, use:

```
make KDIR=/lib/modules/4.18.12-arch1-1-ARCH/build INSTALL_MOD_DIR=updates/tbsusb modules_install
```

## Raspberry Pi

A TBS 5990 connected to a RPi4 prevents it from powering up or rebooting due to backpowering of the
USB port (I guess). A simple fix is to disable PIN1 (+5V) of the USB cable. I did it with a small
strip of hockey tape which I put on PIN1 (upper left) of the plug connected with the TBS 5990.
