# Contiki Toolchain for Arch Linux installation

## Getting started
Setting up the Contiki toolchain in Arch Linux is a *2 step process*:
1. installing packages that are required to run and build Contiki's examples/simulations;
2. cloning the Contiki repository from GitHub (<https://github.com/contiki-os/contiki>).

## Step 1: Contiki dependencies
The packages that Contiki depends on are 32-bit, although 64-bit processors are backwards compatible with 32-bit, thus running 32-bit software is possible on 64-bit Arch Linux.
All except one of Contiki's dependencies can be installed from Arch Linux's official repositories (core, extra, community, multilib). That one package is the `gcc-msp430` compiler set. (see bellow).

### Packages from official repositories
Install the required packages. First though, the `multilib` repository must be enabled in `/etc/pacman.conf`. Make sure that the following lines are uncommented:
```
[multilib]
Include = /etc/pacman.d/mirrorlist
```

Next, update local package database (double `y` enforces updating the package list even if it's considered up-to-date):
```sh
[sudo] pacman -Syy
```

Now, install the packages:
```
[sudo] pacman -S libmpc zlib apache-ant jdk8-openjdk arm-none-eabi-gcc arm-none-eabi-gdb lib32-gcc-libs lib32-glibc lib32-libstdc++5 lib32-zlib lib32-fakeroot
```

### `gcc-msp430` compiler set
In order to use MSP430 based platforms you need to install the gcc-msp430 package **VERSION <= 4.7.x** (version used in this guide: 4.7.2) which is available in *Ubuntu*.
There is a `mspgcc-ti` package available in [AUR](https://aur.archlinux.org/packages/mspgcc-ti/), however it provides GCC **in version >= 6.x** which Contiki is currently not compatible with.

There also is the `gcc-msp430` package available, but it's not compatible with Contiki either (most likely simple mismatched paths).

A prebuilt pacman package `gcc-msp430-bin`, based on [this build](https://github.com/alexkrontiris/Setup-Contiki-Toolchain-in-Arch-Linux) by [alexkrontiris](https://github.com/alexkrontiris), is available here:
* https://drive.google.com/file/d/1223IJ8jrsj9Nk9LQIFrGNo9R5WTR-IQv/view?usp=sharing
* https://github.com/mjbogusz/contiki-toolchain-archlinux

#### Installation
To install it, download the file `gcc-msp430-bin-4.7.2-1-x86_64.pkg.tar.xz`, verify it's sha256 sum using command:
```sh
sha256sum gcc-msp430-bin-4.7.2-1-x86_64.pkg.tar.xz
```
which should output:
```
f6d7d81991164e1c0b4b68a0bf018daca9fe65bd5fe12d6b5aea3da7b99f827c  gcc-msp430-bin-4.7.2-1-x86_64.pkg.tar.xz
```

Then, install the package using pacman:
```sh
[sudo] pacman -U gcc-msp430-bin-4.7.2-1-x86_64.pkg.tar.xz
```

and verify the installation by running the following command:
```sh
$ msp430-gcc --version
```
which should output:
```
msp430-gcc (GCC) 4.7.2 20120920 (mspgcc dev 20120911)
Copyright (C) 2012 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## Step 2: Cloning Contiki
Clone the Contiki GitHub repository to a local directory:
```sh
git clone https://github.com/contiki-os/contiki.git
```

Once cloned, initialize git submodules:
```sh
cd contiki/
git submodule update --init
```

## DONE
Try openning a simulation in *cooja* and see if it runs.

## Tips and tricks
Instead of doing `cd /path/to/cooja` and then `ant run` each time you run *cooja*, you could create an *alias* in your `.bashrc` like this: `alias cooja='sh -c "cd /path/to/cooja && ant run"'`.
