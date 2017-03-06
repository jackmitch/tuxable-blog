+++
date = "2017-03-05T10:00:00Z"
title = "ASUS Tinker Board Overview"
menu = ""
Categories = ["Boards","Tinker"]
Tags = ["tinker", "devboard"]
Description = ""
featuredImage = "/images/tinkerboard.jpg"
+++

The ASUS Tinkerboard is yet another ARM based, hobbist orientated development
board. It features the quad core 32bit Rockchip RK3288 SoC and takes the
exact same form factor as the Raspberry Pi, along with pin for pin header
compatibility. This means that all the current Raspberry Pi cases will be
compatible and subject to software support the same can be said for any
extension boards.

<!--more-->

{{< figure src="/images/tinkerboard.jpg" >}}

## Hardware

The board features:

- RK3288 SoC
- 2GB RAM
- 4 x USB 2.0 ports
- 3.5mm Audio Jack
- HDMI 2.0
- 1 x MIPI DSI
- 1 x MIPI CSI
- 1 x 10/100/1000 Ethernet Port
- Wifi B/G/N
- BT 4.0
- PWM Contact Points
- S/PDIF Contact Points

A Raspberry Pi pin compatible header is also exposed with a mixture of
combinations for digital I/O.

#### CPU/GPU

RK3288 SoC

<cite>[Wikipedia - Rockchip RK3288](https://en.wikipedia.org/wiki/Rockchip_RK3288#Specifications)</cite>

```text
- 28 nm HKMG process.
- Quad-core ARM Cortex-A17, up to 1.8 GHz
- Quad-core ARM Mali-T760 MP4 GPU clocked at 600 MHz
     supporting OpenGL ES 1.1/2.0/3.0/3.1, OpenCL 1.1,
     Renderscript and Direct3D 11.1
- High performance dedicated 2D processor
- 1080P video encoding for H.264 and VP8, MVC
- 4K H.264 and 10bits H.265 video decode, 1080P multi video decode
- Supports 4Kx2K H.265 resolution
- Dual-channel 64-bit DRAM controller supporting DDR3, DDR3L,
     LPDDR2 and LPDDR3
- Up to 3840x2160 display output, HDMI 2.0
- Support dual-channel LVDS/dual-channel MIPI-DSI/eDP1.1
- HW Security system, support HDCP 2.X
- Embedded 13M ISP and MIPI-CSI2 interface
```

#### RAM

2GB LPDDR3 Dual Channel

#### Ethernet

Realtek RTL8211E-VB-CG - Gigabit Ethernet

#### Wifi/BT

Azureware AW-NB177NF - 802.11 B/G/N + Bluetooth v4.0

#### Audio

Realtek RTL ALC4040 24bit 192kHz
