---
layout: post
title: How to convert native trace to LTTng trace and analyze it in Trace Compass?
---

The metadata is an important file which is written in TSDL language. The metadata
has the the description about the native trace. It defines the structure of native
trace. 

If the metadata exactly defines the structure of native trace then the trace can be
analyzed in the babeltrace and the Trace Compass. 

**Important Parts of LTTng to convert the native trace to LTTng trace:** 

**1) trace object:** It has CTF version, packet.header etc.

{% highlight c %}

trace {
    major = 1;
    minor = 8;
    uuid = "6a7715d0-b502-4c65-8678-6777ac7f755a";
    byte_order = le;
    packet.header := struct {
        uint32_t magic;
        uint8_t  uuid[16];
        uint32_t stream_id;
        uint64_t stream_instance_id;
    };
};

{% endhighlight %}

**2) env object:** It define the hostname,trace name etc.

{% highlight c %}

env {
	hostname = "Record_Item";
	domain = "kernel";
	sysname = "Linux";
	kernel_release = "4.18.14-arch1-1-ARCH";
	kernel_version = "#1 SMP PREEMPT Sat Thu 17 13:42:37 UTC 2019";
	tracer_name = "lttng-modules";
	tracer_major = 2;
	tracer_minor = 11;
	tracer_patchlevel = 0;
};

{% endhighlight %}

**3) clock object:** It define the clock's frequency, offset etc.

{% highlight c %}

clock {
    name = "monotonic";
    uuid = "234d669d-7651-4bc1-a7fd-af581ecc6232";
    description = "Monotonic Clock";
    freq = 1000000000; /* Frequency, in Hz */
    /* clock value offset from Epoch is: offset * (1/freq) */
    offset = 1539783991179109789;
};

typealias integer {
	size = 27; align = 1; signed = false;
	map = clock.monotonic.value;
} := uint27_clock_monotonic_t;

typealias integer {
	size = 32; align = 8; signed = false;
	map = clock.monotonic.value;
} := uint32_clock_monotonic_t;

typealias integer {
	size = 64; align = 8; signed = false;
	map = clock.monotonic.value;
} := uint64_clock_monotonic_t;

{% endhighlight %}

**4) packet.context object:** It define the timestamp, content size, packet size etc.

{% highlight c %}

struct packet_context {
	uint64_clock_monotonic_t timestamp_begin;
	uint64_clock_monotonic_t timestamp_end;
    uint64_t content_size;
	uint64_t packet_size;
    uint64_t packet_seq_num;
	unsigned long events_discarded;
	uint32_t cpu_id;
};

{% endhighlight %}

**4) event.header object:** There are two types of event.header one is event_header_compact
and another one is event_header_large.

{% highlight c %}

struct event_header_compact {
	enum : uint5_t { compact = 0 ... 30, extended = 31 } id;
	variant <id> {
		struct {
			uint27_clock_monotonic_t timestamp;
		} compact;
		struct {
			uint32_t id;
			uint64_clock_monotonic_t timestamp;
		} extended;
	} v;
} align(8);

struct event_header_large {
	enum : uint16_t { compact = 0 ... 65534, extended = 65535 } id;
	variant <id> {
		struct {
			uint32_clock_monotonic_t timestamp;
		} compact;
		struct {
			uint32_t id;
			uint64_clock_monotonic_t timestamp;
		} extended;
	} v;
} align(8);

{% endhighlight %}

**5) stream object:** It inclues event.header and packet.context.

{% highlight c %}

stream {
    id = 0;
    event.header := struct event_header_compact;
    packet.context := struct packet_context;
};

{% endhighlight %}

**5) event object:** It define the event of trace and the metadata can have many events.

{% highlight c %}

event {
    name = "sched_switch";
    id = 0;
    stream_id = 0;
    fields := struct {
        integer { size = 8; align = 8; signed = 0; encoding = UTF8; base = 10;} _prev_comm[16];
        integer { size = 32; align = 8; signed = 1; encoding = none; base = 10; } _prev_tid;
        integer { size = 32; align = 8; signed = 1; encoding = none; base = 10; } _prev_prio;
        integer { size = 64; align = 8; signed = 1; encoding = none; base = 10; } _prev_state;
        integer { size = 8; align = 8; signed = 0; encoding = UTF8; base = 10; } _next_comm[16];
        integer { size = 32; align = 8; signed = 1; encoding = none; base = 10; } _next_tid;
        integer { size = 32; align = 8; signed = 1; encoding = none; base = 10; } _next_prio;
    };
};

{% endhighlight %}

# References

[Trace Compass](https://www.eclipse.org/tracecompass/)

[LTTng](https://lttng.org/docs/v2.10/)

[babeltrace](http://diamon.org/babeltrace/)

[CTF](http://diamon.org/ctf/#ctf-in-a-nutshell)

[rtems-tools](https://github.com/rmeena840/rtems-tools/tree/ravindra-rtems)
