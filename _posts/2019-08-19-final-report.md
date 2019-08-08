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


