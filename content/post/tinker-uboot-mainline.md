+++
menu = ""
Categories = ["Boards", "Tinker"]
Tags = ["mainline","uboot","tinker"]
Description = "Booting mainline uboot on the ASUS Tinker board"
date = "2017-03-05T12:00:00Z"
title = "Mainline UBoot on the ASUS Tinker Board"

+++

The ASUS Tinker board can boot mainline u-boot with a couple of pending
patches applied. As the board doesn't feature any on-board storage such as
eMMC or Flash, the u-boot binaries must be written to the uSD card.

<!--more-->

First clone, checkout and apply the required patches

```text
$ git clone git://git.denx.de/u-boot.git u-boot.git

$ cd u-boot.git

$ git checkout 3fd2b3aa19b9479b5e785087e4951d3a7bbb87be

$ curl -O -J https://patchwork.ozlabs.org/patch/731367/raw
$ curl -O -J https://patchwork.ozlabs.org/patch/731370/raw
$ curl -O -J https://patchwork.ozlabs.org/patch/729823/raw

$ git am *.patch
```

If you're cross compiling, ensure you have your CROSS_COMPILE environment
variable set correctly, then proceed to compile.

```text
$ echo ${CROSS_COMPILE}
$ arm-oe-linux-gnueabi-

$ make tinker-rk3288_defconfig
$ make -j4
```

Once this has sucessfully built the binaries they must be built into a Rockchip
compatible format.

```text
$ ./tools/mkimage -n rk3288 -T rksd -d spl/u-boot-spl-dtb.bin out
$ cat u-boot-dtb.bin >> out
```

We can then flash the resulting image to the uSD card.

```text
$ dd if=out of=/dev/sdc seek=64
```

If you have the serial connected to your Tinker board you should now see your
newly compiled u-boot prompt. UART2 on pins 32 and 33 is the default UART on
mainline u-boot.

```text
U-Boot SPL 2017.03-rc3-00005-g79bf183-dirty (Mar 05 2017 - 11:17:43)

U-Boot 2017.03-rc3-00005-g79bf183-dirty (Mar 05 2017 - 11:17:43 +0000)

Model: Tinker-RK3288
DRAM:  2 GiB
MMC:   dwmmc@ff0c0000: 1
MMC Device 0 not found
```
