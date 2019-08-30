# TBS USB drivers

These are out-of-tree modules and do not require a full v4l media tree.
Only required modules are built to add support for TBS cards in the cx231xx
module. This is only tested with ArchLinux (kernel 4.19 and 5.2).

Reason for not using the full media build from tbstv are:

* The second adapter never worked on my Raspberry Pi4
* It prevented loading some Pi4 specific modules
* It takes too long to build after a kernel upgrade

So far no issues have been detected. My TBS 5990 runs with both adapters
for quite some time now.

This repository is heavily inspired by https://github.com/AlexanderS/tbsecp3-driver.

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

## TODO

* ArchLinux dkms package

