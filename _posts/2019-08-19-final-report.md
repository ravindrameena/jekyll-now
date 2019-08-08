---
layout: post
title: GSoC 2019 Final Report
---

![_config.yml]({{ https://rmeena840.github.io/ }}/images/rtems.png)

This report summarizes the work that I have done during Google Summer of Code 2019 period 
and what is left to do.

# Contact Information:

**Name:** Ravindra Kumar Meena

**University:** Indian Institute of Technology(ISM), Dhanbad

**IRC nickname:** rmeena840

**Email:** rmeena840@gmail.com

# Project details:

**Project title:** Basic Support for Trace Compass (ticket: [#3696](https://devel.rtems.org/ticket/3696))

**Proposal link:** [Here](https://docs.google.com/document/d/
1G6ISV_vIYLKl5Em2lwF8W91YrHWkve2KRSPOolerjTg/edit)

**Weekly Updates:** [Here](https://devel.rtems.org/wiki/GSoC/2019#RavindraKumarMeena)

**GitHub Repository:** [rtems-tools](https://github.com/rmeena840/rtems-tools/tree/ravindra-rtems), 
[rtems-docs](https://github.com/rmeena840/rtems-docs/tree/ravindra-rtems)

# Project Abstract:

The goal of this project is to enable the Trace Compass to analyze and display some basic 
information using Event Recording infrastructure. Trace Compass is a software for viewing and 
analyzing any type of logs or traces. The basic information to analyze and display information 
include CPU usage, IRQ analysis(IRQ Statistics, IRQ Table, IRQ vs Count, IRQ vs Time), Linux Kernel
(Control Flow, Resources) etc.

# Mentors:

**\*** Sebastian Huber

**\*** Gedare Bloom

**\*** Chris Johns

# Project Objectives:

There are three main objectives of the project:

**1.)** Store the event streams per CPU received from RTEMS target in disk.

**2.)** Write the LTTng metadata for the event stream per CPU stored in disk.

**3.)** Add the sched_switch event in both LTTng metadata and client-side so that
Trace Compass can display both CPU usage and resources graph.

# What was done:

## During GSoC Phase 1:

**1.)** Patch for event recording docs. [Patch-link](https://github.com/rmeena840/rtems-docs/commit/
b8889a84645d2a4bed8f94a5888083d93ff08b20)

**2.)** Patch for Event Recording Trace generation example. [Patch-link](https://github.com/
rmeena840/rtems-docs/commit/68e2239548dac48f533572152a5c8033ff2122b6)

**3.)** Patch for writing event stream from RTEMS target in a file. [Patch-link](https://github.com/
rmeena840/rtems-tools/commit/f68b5031f4e6f847239effe677701635316b12fb)

**4.)** Patch for metadata which is compatible with generated event stream from RTEMS target.
[Patch-link](https://github.com/rmeena840/rtems-tools/commit/
c0035feab6d99b4aeecdd0d76b049f3e2c7aa9ef)

**Main Outcome of Phase 1:** The babeltrace can read and print the event streams generated 
from RTEMS target.

## During GSoC Phase 2:

**1.)** Record a raw record item stream produced by the Qemu target via the nc tool in a file (not 
more than 100KiB) and add this file to rtems-tools. [Patch-link](https://github.com/rmeena840/
rtems-docs/commit/b8889a84645d2a4bed8f94a5888083d93ff08b20)

**2.)** Modified the client-side program to read from a file if a --input=<FILE> command line 
option is given. [Patch-link](https://github.com/rmeena840/rtems-docs/commit/
68e2239548dac48f533572152a5c8033ff2122b6)

**3.)** Open event stream file for each processor and write events of CPU to the corresponding file 
opened for each CPU. [Patch-link](https://github.com/rmeena840/rtems-tools/commit/
f68b5031f4e6f847239effe677701635316b12fb)

**4.)** Patch for LTTng metadata [Patch-link](https://github.com/rmeena840/rtems-tools/commit/
c0035feab6d99b4aeecdd0d76b049f3e2c7aa9ef). In this patch LTTng components were added like
packet.header, packet.context etc. 

**5.)** Patch for modified client-side program which is compatible with LTTng metadata [Patch-link]
(https://github.com/rmeena840/rtems-tools/commit/c0035feab6d99b4aeecdd0d76b049f3e2c7aa9ef)

**Main Outcome of Phase 2:** Client-side program now have support to read from a file if a
--input=<FILE> command line option is given. Earlier only babeltrace was able to read the event stream but now Trace Compass can also read event stream values. The Trace Compass can also
display the CPU usage and resources.

## During GSoC Phase 3:

**1.)** Detected the IDLE/RUNNING state of thread and set the value according to thread state(IDLE/
RUNNING). [Patch-link](https://github.com/rmeena840/rtems-docs/commit/
b8889a84645d2a4bed8f94a5888083d93ff08b20)

**2.)** Retrieved thread id and thread names from RTEMS target and stored in the table and 
populated the table to sched_switch event in client-side so that thread can have the name. 
[Patch-link](https://github.com/rmeena840/rtems-docs/commit/
68e2239548dac48f533572152a5c8033ff2122b6)

**3.)** Generated metadata from client-side. [Patch-link](https://github.com/rmeena840/rtems-tools/
commit/f68b5031f4e6f847239effe677701635316b12fb)

**Main Outcome of Phase 3:** Client-side program now have support to read from a file if a
--input=<FILE> command line option is given. Earlier only babeltrace was able to read the event stream but now Trace Compass can also read event stream values. The Trace Compass can also
display the CPU usage and resources.

# What is left – Bugs and Further Enhancements

# Acknowledgment

So this is it – the end of the official GSoC coding period. Thank you to the Google Summer of Code 
Team and the RTEMS community for bringing this project to life, and of course huge thanks to my 
mentors Sebastian Huber, Gedare Bloom and Chris Johns for their feedback and guidance throughout 
the entire project.  I would further like to extend my deep gratitude towards our RTEMS 
organization admins, Dr. Joel Sherrill, Gedare Bloom and Chris Johns for their valuable inputs 
and support.  Special thanks to LTTng community for their wonderful reviews and generosity.

Altogether, this was a great experience and I will remain an active contributor for the foreseeable 
future. Happy coding!
