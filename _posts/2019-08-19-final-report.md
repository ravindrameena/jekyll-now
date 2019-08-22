---
layout: post
title: GSoC 2019 Final Report
---

![_config.yml]({{ https://rmeena840.github.io/ }}/images/rtems.png)

This report summarizes the work that I have done during Google Summer of Code 2019 period 
and what is left to do.

# Contact Information:

**Name:** Ravindra Kumar Meena

**University:** Indian Institute of Technology (ISM), Dhanbad

**IRC nickname:** rmeena840

**Email:** rmeena840@gmail.com

**GitHub handle:** rmeena840

# Project details:

**Project title:** Basic Support for Trace Compass (ticket: [#3696](https://devel.rtems.org/ticket/3696))

**Proposal link:** [Here](https://docs.google.com/document/d/
1G6ISV_vIYLKl5Em2lwF8W91YrHWkve2KRSPOolerjTg/edit)

**Weekly Updates:** [Here](https://devel.rtems.org/wiki/GSoC/2019#RavindraKumarMeena)

**GSoC blog:** [Blog link](https://rmeena840.github.io/)

# Mentors:

**\*** Sebastian Huber

**\*** Gedare Bloom

**\*** Chris Johns

# Project Abstract:

The goal of this project is to enable the Trace Compass to analyze and display some basic 
information using Event Recording infrastructure. Trace Compass is a software for viewing and 
analyzing any type of logs or traces. The basic information to analyze and display information 
include CPU usage, IRQ analysis(IRQ Statistics, IRQ Table, IRQ vs Count, IRQ vs Time), Linux Kernel
(Control Flow, Resources) etc. Linux Kernel trace graph view in Trace Compass depends on
sched_switch event of LTTng metadata which is used with RTEMS target trace to view the trace 
graph.

**RTEMS wiki of GSoC project:** [wiki](https://devel.rtems.org/wiki/GSoC/2019/Basic_Support_for_Trace_Compass)

**Develooment branch on GitHub:** [rtems-tools](https://github.com/rmeena840/rtems-tools/commits/
ravindra-rtems), 
[rtems-docs](https://github.com/rmeena840/rtems-docs/commits/master)

# GSoC project main Objective:

There are three main objectives of the project:

**1.)** Store the event streams per CPU received from RTEMS target on the host’s disk.

**2.)** Write the LTTng metadata for the event stream per CPU stored on the host's
disk.

**3.)** Add the sched_switch event in both LTTng metadata and client-side so that
Trace Compass can display both CPU usage and resources graph.

# GSoC project previous state:

![_config.yml]({{ https://rmeena840.github.io/ }}/images/recording-previous-state.png)

On successfully getting host connected to the target. The target produces the TCP streams to the 
host which is not in LTTng format.

# GSoC project current state:

![_config.yml]({{ https://rmeena840.github.io/ }}/images/event-recording-trace.png)

On successfully getting host connected to the target. The target produces the TCP streams to the 
host which is converted into LTTng trace on the host side. The Trace Compass and babeltrace are two 
software that can read the LTTng trace. The babeltrace can only print the LTTng trace whereas, 
Trace Compass can display CPU usage and resources.

# What was done in three GSoC phases:

The GSoC project was divided into three phases. 

## During GSoC Phase 1:

**1.)** Patch ( for rtems-docs, tracing section ) for trace generation example from RTEMS target. This 
patch was on the basis of the current state of the project. [Patch-link](https://github.com/rmeena840/rtems-docs/commit/73aaf8ab381a2794fbf2fc0098896696c74b6819)

**2.)** Writing record items from RTEMS target in a file stored on the host’s disk.

**3.)** Wrote metadata which is compatible with generated event stream from RTEMS target.

**Main Outcome of Phase 1:** The babeltrace can read and print the event streams generated 
from RTEMS target.

## During GSoC Phase 2:

**1.)** Recorded a raw record item stream produced by the Qemu target via the nc tool in a file 
(not more than 100KiB) and add this file to rtems-tools.

**2.)** Modified the client-side program to read from a file if a –input= command-line option is 
given.

**3.)** Open event stream files for each processor and write events of CPU to the corresponding 
file opened for each CPU.

**4.)** Produced LTTng metadata. In these LTTng components like packet.header, packet.context etc 
were added. 

**5.)** Modified client-side program which is compatible with LTTng metadata.

**6.)** Added sched_switch in both client-side and LTTng metadata.

**Main Outcome of Phase 2:** The Client-side program now has support to read from a file if –input= 
command-line option is given. Earlier only babeltrace was able to read the event stream but now 
Trace Compass can also read event stream values. The Trace Compass can also display the CPU usage 
and resources.

## During GSoC Phase 3:

**1.)** Detected the IDLE/RUNNING state of thread and set the value according to the thread state
(IDLE/ RUNNING).

**2.)** Retrieved thread id and thread names from RTEMS target and stored in the table. 

**3.)** Populated the table to sched_switch event in the client-side so that thread can have the 
name.

**4.)** Generated metadata from the client-side.

**5.)** Produced documentation patch. This documentation patch was on the basis of the final 
stage of the project. [Patch Link](https://github.com/rmeena840/rtems-docs/commit/cbad5f2cd4905cb9d3312cd4ccce222bad8fbaee)

**Main Outcome of Phase 3:** The Trace Compass can now display the thread state (IDLE/RUNNING) 
and thread names. The client-side program can now generate LTTng metadata.

## Trace Compass CPU usage and resource snapshot:

![_config.yml]({{ https://rmeena840.github.io/ }}/images/Trace-Compass.png)

The above snapshot shows the CPU usage and resources graph. It is also
displays the thread names.

## Merged patch
[rtems-tools](https://git.rtems.org/rtems-tools/commit/?id=ba6b8af8bbd0120d0c4d77de54f2eb909a6081ea)

The above patch got merged into rtems-tools master branch. This patch contains the overall 
coding work done in phases 1, 2 and 3.

# What is left – Bugs and Further Enhancements

**\*** The output command line feature can be added to the client-side program. With this, the 
traces and metadata can be generated in a particular folder.

**\*** There is no IRQ support yet.

**\*** Advanced support for Trace Compass could include dynamic memory traces, stack usage, network 
packet flow, etc.

# Acknowledgment

So this is it – the end of the official GSoC coding period. Thank you to the Google Summer of Code 
Team and the RTEMS community for bringing this project to life, and of course huge thanks to my 
mentors Sebastian Huber, Gedare Bloom and Chris Johns for their feedback and guidance throughout 
the entire project.  I would further like to extend my deep gratitude towards our RTEMS 
organization admins, Dr. Joel Sherrill, Gedare Bloom and Chris Johns for their valuable inputs 
and support.  Special thanks to LTTng community for their wonderful reviews and generosity.

Altogether, this was a great experience and I will remain an active contributor for the foreseeable 
future. Happy coding!
