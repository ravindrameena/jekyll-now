---
layout: post
title: Building LibBSD for RTEMS using Waf
---

Welcome to building LibBSD for RTEMS using Waf. This package is a library containing various parts of the FreeBSD kernel ported to RTEMS. The library replaces the networking port of FreeBSD in the RTEMS kernel sources.

The following instructions show you how to build and install RTEMS Tools and RTEMS kernel for your BSP in separate paths. The Waf build support for RTEMS requires you provide your BSP name as an architecture and BSP pair. 

We will build an Xilinx Zynq QEMU BSP using the arm/xilinx_zynq_a9_qemu.

**1.** Create a sandbox directory

{% highlight c %}

 $ sandbox="$PWD/sandbox"
 $ mkdir sandb

{% endhighlight %}

**2.** Clone the repositories: 

{% highlight c %}

$ cd "$sandbox"
$ git clone git://git.rtems.org/rtems-source-builder.git
$ git clone git://git.rtems.org/rtems.git
$ git clone git://git.rtems.org/rtems-libbsd.git

{% endhighlight %}

**3.** Build and install the tools: 

{% highlight c %}

$ cd "$sandbox"
$ cd rtems-source-builder/rtems
$ ../source-builder/sb-set-builder --prefix="$sandbox/rtems/5" 5/rtems-arm

{% endhighlight %}

**4.** Bootstrap the RTEMS sources: 

{% highlight c %}

$ cd "$sandbox"
$ cd rtems
$ PATH="$sandbox/rtems/5/bin:$PATH" ./bootstrap

{% endhighlight %}

**5.** Build and install the RTEMS Board Support Packages (BSP) you want to use: 

{% highlight c %}

$ cd "$sandbox"
$ cd rtems
$ PATH="$sandbox/rtems/5/bin:$PATH" ./bootstrap

{% endhighlight %}

**6.** Populate the rtems_waf git submodule. Note, make sure you specify 'rtems_waf' or the FreeBSD kernel source will be cloned: 

{% highlight c %}

$ cd "$sandbox"
$ cd rtems-libbsd
$ git submodule init
$ git submodule update rtems_waf

{% endhighlight %}

**7.** Run Waf's configure with your specific settings. In this case the path to the tools and RTEMS are provided on the command line and so do not need to be in your path or environment. You can use '--rtems-archs=arm,sparc,i386' or '--rtems-bsps=arm/xilinx_zynq_a9_qemu,sparc/sis,i386/pc586' to build for more than BSP at a time. 

{% highlight c %}

$ cd "$sandbox"
$ cd rtems-libbsd
$ ./waf configure --prefix="$sandbox/rtems/5" \
    --rtems-bsps=arm/xilinx_zynq_a9_qemu \
    --buildset=buildset/default.ini

{% endhighlight %}

**8.** Build and install: 

{% highlight c %}

$ cd "$sandbox"
$ cd rtems-libbsd
$ ./waf
$ ./waf install

{% endhighlight %}  

**9.** Run the tests on QEMU, for example: 

{% highlight c %}

$ qemu-system-arm -no-reboot -serial null -serial mon:stdio -net none \
   -nographic -M xilinx-zynq-a9 -m 256M \
   -kernel build/arm-rtems5-xilinx_zynq_a9_qemu-default/selectpollkqueue01.exe

{% endhighlight %}  

# Qemu and Networking

You can use the Qemu simulator to run a LibBSD based application and connect it to a virtual network on your host. You have to create a TAP virtual Ethernet interface for this:

{% highlight c %}

$ sudo tunctl -p -t qtap -u $(whoami)
$ sudo ip link set dev qtap up
$ sudo ip addr add 169.254.1.1/16 dev qtap

{% endhighlight %} 

You can show the interface state with the following command:

{% highlight c %}

$ ip addr show qtap

{% endhighlight %} 

You may have to assign the interface to a firewall zone.

The Qemu command line varies by board support package, here is an example for the arm/xilinx_zynq_a9_qemu BSP:

{% highlight c %}

$ qemu-system-arm -serial null -serial mon:stdio -nographic \
  -M xilinx-zynq-a9 -m 256M \
  -net tap,ifname=qtap,script=no,downscript=no \
  -net nic,model=cadence_gem,macaddr=0e:b0:ba:5e:ba:12 \
  -kernel build/arm-rtems5-xilinx_zynq_a9_qemu-default/media01.exe

{% endhighlight %} 

After some seconds it will acquire a IPv4 link-local address, e.g.

{% highlight c %}

info: cgem0: probing for an IPv4LL address
debug: cgem0: checking for 169.254.159.156

{% endhighlight %} 

You can connect to the target via telnet for example:

{% highlight c %}

$ telnet 169.254.159.156
Trying 169.254.159.156...
Connected to 169.254.159.156.
Escape character is '^]'.

RTEMS Shell on /dev/pty4. Use 'help' to list commands.
TLNT [/] #

{% endhighlight %} 

If you get the above output "Connected 169.254.159.156" then you have successfully connected the host to the target.

# References

[RTEMs-libbsd](https://github.com/RTEMS/rtems-libbsd)
