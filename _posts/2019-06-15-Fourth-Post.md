---
layout: post
title: RTEMS Trace Item Generation Example
---

This post will guide you through how to generate RTEMS record item from and send it back to
host.

Step 1: Clone the following repositories and set up the development environment

{% highlight c %}

$ cd "$sandbox"
$ git clone https://github.com/rmeena840/rtems-libbsd/tree/ravindra-rtems
$ git clone https://github.com/rmeena840/rtems-tools/tree/ravindra-rtems

{% endhighlight %}

Step 2: The Qemu command line varies by board support package, here is an
example for the arm/xilinx_zynq_a9_qemu BSP:

{% highlight c %}

  cd rtems-libbsd

  qemu-system-arm -serial null -serial mon:stdio -nographic \
  -M xilinx-zynq-a9 -m 256M \
  -net tap,ifname=qtap,script=no,downscript=no \
  -net nic,model=cadence_gem,macaddr=0e:b0:ba:5e:ba:12 \
  -kernel build/arm-rtems5-xilinx_zynq_a9_qemu-default/media01.exe

{% endhighlight %}

Step 3: This requires to TAP virtual Ethernet interface for this:

{% highlight c %}

  sudo tunctl -p -t qtap -u $(whoami)
  sudo ip link set dev qtap up
  sudo ip addr add 169.254.1.1/16 dev qtap

{% endhighlight %}

After some seconds it will acquire a IPv4 link-local address, e.g.

{% highlight c %}

  info: cgem0: probing for an IPv4LL address
  debug: cgem0: checking for 169.254.XXX.XXX

{% endhighlight %}

Use telnet command to connect host to target.

{% highlight c %}

 telnet 169.254.XXX.XXX

{% endhighlight %}

Step 4: After successfully connected to the target, we can get event records
item  from QEMU target text format by using the following commands:

{% highlight c %}

  cd rtems-tools
  ./build/misc/rtems-record -H 169.254.XXX.XXX -p 1234 | head

{% endhighlight %}

The received trace generated on host will look like this:

{% highlight c %}

  0.003629099:0:THREAD_SWITCH_OUT:9010001
  0.003629099:0:THREAD_STACK_CURRENT:e68
  0.003629099:0:THREAD_SWITCH_IN:a010005
  0.003847169:0:THREAD_SWITCH_OUT:a010005
  0.003847169:0:THREAD_STACK_CURRENT:7ea8
  0.003847169:0:THREAD_SWITCH_IN:9010001
  0.004627569:0:THREAD_SWITCH_OUT:9010001
  0.004627569:0:THREAD_STACK_CURRENT:e68
  0.004627569:0:THREAD_SWITCH_IN:a010005
  0.004912869:0:THREAD_SWITCH_OUT:a010005

{% endhighlight %}

The received event records items is not in CTF format.
