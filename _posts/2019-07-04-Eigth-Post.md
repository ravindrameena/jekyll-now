---
layout: post
title: What is babeltrace and what it has to do with CTF?
---

In order to implement these use cases with the tracing framework we must 
understand the underlying technologies used along with it. The two main components 
crucial to realization of tracing are the Common Trace Format (CTF) and babeltrace.

CTF is a binary trace format which is flexible and fast to write. A typical CTF 
trace comprizes of numerous streams of binary events. One can decide the number of 
streams into which the binary events can be divided into. However the metadata 
stream which consists of data about the about the trace is mandatory. Every binary 
stream consists of several packets which contain the trace information or payload. 
The organization of these packets follows an orderly and maybe padded sequence of 
events. Trace Stream Description Language (TSDL) is a descriptive language which 
is used to describe all the header, contexts and event fields of a CTF trace.

Babeltrace is an open source trace format converter as well as the reference 
parser implementation of the Common Trace Format. It was originally used to parse 
CTF traces produced by LTTng and produce readable text output. LTTng is the open 
source tracing framework for Linux operating system.

# References

[babeltrace](http://diamon.org/babeltrace/)

[CTF](http://diamon.org/ctf/#ctf-in-a-nutshell)