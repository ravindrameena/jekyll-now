---
layout: post
title: GSoC 2019 Final Report
---

# Project Overview

The goal of this project is to enable the Trace Compass to analyze and display some basic 
information using Event Recording infrastructure. Trace Compass is a software for viewing and 
analyzing any type of logs or traces. The basic information to analyze and display information 
include CPU usage, IRQ analysis(IRQ Statistics, IRQ Table, IRQ vs Count, IRQ vs Time), Linux Kernel
(Control Flow, Resources) etc.

# Mentors

**.** Sebastian Huber
**.** Gedare Bloom
**.** Chris Johns

# Project Objectives

There are three main objectives of the project.

**1.)** Store the event streams per CPU received from RTEMS target in disk.

**2.)** Write the LTTng metadata for the event stream per CPU stored in disk.

**3.)** Add the sched_switch event in both LTTng metadata and client-side so that
Trace Compass can display both CPU usage and resources graph.


