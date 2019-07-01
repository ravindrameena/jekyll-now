---
layout: post
title: Why would anyone require tracing? 
---

Real time applications follow strict time and performance constraints. Tracing can 
prove to be an efficient debugging tool which can help analyze the performance of 
such applications and identify tricky bugs. Some common issues with real time 
applications for which rtems tracing framework will prove to be useful are modelled as use cases as follows:

1) Detecting deadlock conditions: Real time applications inherently involve 
parallel execution of tasks to provide faster computation and results. However 
there might exist cases when these tasks compete for common resources (eg 
processor time) and enter a circular unending wait. The performance of an 
application under deadlock deteriorates quickly. Hence such conditions must be 
detected timely so that the application programmer can take the necessary steps to 
avert deadlocks.

2) Track complex thread operations including entry and exit events: Threads are 
primarily useful in introducing concurrency of task execution and hence can be a 
vital component to real time applications. However using threads in an application 
is a complex and convoluted task. Tracing framework can prove to be an efficient 
programming tool to track down problems with thread execution. Tracing thread 
creation, deletion, entry and exit operations can be considered as an important 
use case in this regard.

3) Tracing a function: This is a basic tracing paradigm which can be useful in 
case of numerous nested calls to different functions.

4) Tracing user extensions: Tracing user defined extensions in rtems applications 
can also be considered as an important use case for the rtems tracing framework.

5) Detecting race conditions: Another common issue with parallel execution or 
concurrent processing is encountering race conditions. This scenario usually 
occurs when multiple processes enter common critical sections or access and update 
common data structures. There is no way to identify which process’s modification 
will be reflected as the final output. By tracing processes’ execution as well as 
values of common data structures we might be able to analyse the existence of race 
conditions.
