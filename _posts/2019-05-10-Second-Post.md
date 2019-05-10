---
layout: post
title: Building LibBSD for RTEMS using Waf
---

Welcome to building LibBSD for RTEMS using Waf. This package is a library containing various parts of the FreeBSD kernel ported to RTEMS. The library replaces the networking port of FreeBSD in the RTEMS kernel sources.

The following instructions show you how to build and install RTEMS Tools and RTEMS kernel for your BSP in separate paths. The Waf build support for RTEMS requires you provide your BSP name as an architecture and BSP pair. 

We will build an Xilinx Zynq QEMU BSP using the name arm/xilinx_zynq_a9_qemu.

<b>1. Create a sandbox directory</b>
```
$ sandbox="$PWD/sandbox"
$ mkdir sandbox
```