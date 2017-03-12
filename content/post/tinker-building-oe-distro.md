+++
date = "2017-03-11T10:00:00Z"
title = "ASUS Tinker Minimal OpenEmbedded Distro"
menu = ""
Categories = ["Boards","Tinker"]
Tags = ["tinker", "devboard"]
Description = ""
comments = true
+++

Building an OpenEmbedded based distro for the Tinker board is easy to do
with my meta-tinker OpenEmbedded layer hosted on
[github](http://www.github.com/jackmitch/meta-tinker.git"). If you encounter any
errors in building please first refer to the [Yocto Mega Manual](http://www.yoctoproject.org/docs/1.8/mega-manual/mega-manual.html) before opening an issue on github.

#### What is OpenEmbedded

OpenEmbedded is a build framework with which a linux distro can be built
from source. It is made up of a collection of tools and meta data, the main
tool being bitbake, which is used to parse meta data and execute commands.
The core set of meta data which contains recipes to build applications
central to the majority of linux distributions is called oe-core. When we pair
these two repositories with a Board Support Package (BSP) layer we have the
building blocks to create a minimal linux distro for the board the BSP targets.

#### Building an OpenEmbedded Distro for the Tinker

This is a very breif overview and won't go into detail on how a distro is put
together, but you will end up with a tar file which can be extracted onto an uSD
card and boot a minimal distro on the Tinker board. From here you then have the
base to explore customising the build and extending the applications on the
image.

First, clone the required repositories

```text
mkdir oe-tinker
git clone git://git.openembedded.org/bitbake bitbake.git
git clone git://git.openembedded.org/openembedded-core oe-core.git
git clone git://github.com/jackmitch/meta-tinker.git meta-tinker.git
```

Now initialise a new build directory

```text
source oe-core.git/oe-init-build-env build bitbake.git/
```

This should have placed you in a new directory called build. Everytime you want
to execute bitbake you have to source the above file to setup the environment.

Now we need to edit the new configuration files created under the conf directory.

```text
conf/
├── bblayers.conf
├── local.conf
├── sanity_info
└── templateconf.cfg
```

In bblayers.conf, we need to add the meta-tinker BSP layer. In line with the
other layers already present, add the following line with your build path.

```text
##YOUR_OE_BUILD_PATH###/meta-tinker.git
```

We should now be ready to start the build. To do this we need to invoke the
bitbake tool and tell it which recpie to build and for which machine. We want
to build for the tinker and we want to build a full linux image.

```text
MACHINE=tinker bitbake tinker-basic-image
```

Depending on your build machine specifications this can take from a couple of
hours, to the best part of a day. In brief, this command is parsing all the meta
data from our layers added in bblayers.conf. It is then going off to the internet
and downloading all the sources for the application recipes, and finally
comnfiguiring and building recipes. Everything is built from source, all the way
from the cross-compiler to system applications which is why it can take a while!

Once the build has finished it will have created a tar file which is the full
linux distro image including kernel and applications. It will also have created
a u-boot binary which can boot the board from it's initial bootloader. Now we
flash the uSD card and we will have a booting board!

In the commands below ensure you replace sdX with your uSD device, and also
make sure that the directory /mnt/tmp or a location of your choice to mount to
exists.

```text
dd if=tmp-glibc/deploy/images/tinkerboard/u-boot.bin of=/dev/sdX seek=64
mount /dev/sdX /mnt/tmp
tar xf tmp-glibc/deploy/images/tinkerboard/tinkerboard-basic-image-tinkerboard.tar.gz -C /mnt/tmp
umount /dev/sdX
```

You should now be able to put the uSD card into the Tinker and a very minimal
image will boot. This is just intended to be a base image and any extra
functionality required needs to be added by yourself. The image unfortunatly
does not support the graphics chip.
