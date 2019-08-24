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
