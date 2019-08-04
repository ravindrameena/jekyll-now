---
layout: post
title: What is LTTng?
---

The Linux Trace Toolkit: next generation is an open source software toolkit which you can use to 
simultaneously trace the Linux kernel, user applications, and user libraries.

LTTng consists of:

1.) Kernel modules to trace the Linux kernel.

2.) Shared libraries to trace user applications written in C or C++.

3.) Java packages to trace Java applications which use java.util.logging or Apache log4j 1.2.

4.) A Python package to trace Python applications which use the standard logging package

5.) A kernel module to trace shell scripts and other user applications without a dedicated 
instrumentation mechanism.

6.) Daemons and a command-line tool, lttng, to control the LTTng tracers.

The main distinctive features of LTTng is that it produces correlated kernel and user space traces, 
as well as doing so with the lowest overhead amongst other solutions. It produces trace files in 
the CTF format, a file format optimized for the production and analyses of multi-gigabyte data.

# References

[LTTng](https://lttng.org/docs/v2.10/)

[babeltrace](http://diamon.org/babeltrace/)

[CTF](http://diamon.org/ctf/#ctf-in-a-nutshell)

[rtems-tools](https://github.com/rmeena840/rtems-tools/tree/ravindra-rtems)
