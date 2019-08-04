---
layout: post
title: What is Trace Compass?
---

Eclipse Trace Compass is an open source application to solve performance and reliability issues by 
reading and analyzing traces and logs of a system. Its goal is to provide views, graphs, metrics, 
and more to help extract useful information from traces, in a way that is more user-friendly and 
informative than huge text dumps.

**Important features of Trace Compass:**

**1.) Call Stack:** If you can define trace events representing function entries and exits, you can 
display the call stack of your application over time. You can also get profiling information from 
the Flame Graph or descriptive statistics.

**2.) KERNEL ANALYSIS:** Displays the states of processes and resources over time, using 
information from Linux kernel traces.

**3.) UST MEMORY:** Using LTTng-UST's C standard library wrapper, all calls to memory allocation 
and free are traced. You can display the memory utilization or find potential memory leaks.

**4.) EXTEND TRACE TYPES:** The base framework can be extended to add support for new trace types. 
Support for libpcap traces (the format used by Wireshark) was added this way.

**Benefits of Trace Compass:**

**1.)** Reduce time to identify faults

**2.)** Observe multi-core, heterogeneous, virtualized, and distributed systems

**3.)** Use the same analysis tool for development, testing, and production

**4.)** Extend the framework to fit the needs of your organization

**5.)** Avoid vendor lock-in by using an open source solution

# References

[Trace Compass](https://www.eclipse.org/tracecompass/)

[LTTng](https://lttng.org/docs/v2.10/)

[babeltrace](http://diamon.org/babeltrace/)

[CTF](http://diamon.org/ctf/#ctf-in-a-nutshell)

[rtems-tools](https://github.com/rmeena840/rtems-tools/tree/ravindra-rtems)
