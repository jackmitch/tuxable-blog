+++
date = "2017-03-05T14:00:00Z"
title = "Mainline Linux on the ASUS Tinker Board"
menu = ""
Categories = ["Boards","Tinker"]
Tags = ["kernel","mainline","tinker"]
Description = "Building mainline Linux for the ASUS Tinker board"
comments = true
+++

The ASUS Tinker board can boot mainline linux without any additional
patches, currently a for-next branch targetting 4.12 is required, but
that will change when 4.12 is officially released.

<!--more-->

First clone, checkout a stable tag.

```text
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/mmind/linux-rockchip.git linux.git

$ cd linux.git

$ git checkout v4.12-armsoc/dts32
```

If you're cross compiling, ensure you have your CROSS_COMPILE and ARCH
environment variable set correctly, then proceed to compile.

```text
$ echo ${CROSS_COMPILE}
arm-oe-linux-gnueabi-

$ echo ${ARCH}
arm

$ make multi_v7_defconfig
$ make -j4 zImage dtbs modules
```

Once sucessfully built you can then install them if you're building natively or
copy the resulting binarys onto your uSD card.

```text
$ make INSTALL_MOD_PATH=modules modules_install

$ mount /dev/sdX1 /mnt/boot
$ mount /dev/sdX2 /mnt/root

$ cp arch/arm/boot/zImage arch/arm/boot/dts/rk3288-tinker.dtb /mnt/boot/
$ cp -a modules/* /mnt/root/
```

Ensure your u-boot is looking for the correct dtb and kernel image, then boot
the Tinker board into your fresh upstream kernel!

```text
$ uname -a
Linux tinkerboard 4.10.0-10333-g63700c1de415 #1 SMP Sun Mar 5 15:56:37 GMT 2017 armv7l GNU/Linux
```
