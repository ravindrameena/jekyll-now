---
layout: post
title: What is sched_switch in metadata?
---

sched_switch event defined in the metadata helps to identify if the thread is running or idle
state. 

# sched_switch looks like this:

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

# A thread can have following types of state:

{% highlight c %}

define TASK_RUNNING			    0x0000
define TASK_INTERRUPTIBLE		0x0001
define TASK_UNINTERRUPTIBLE	    0x0002
define TASK_PARKED			    0x0040
define TASK_DEAD			    0x0080
define TASK_WAKEKILL			0x0100
define TASK_WAKING			    0x0200
define TASK_NOLOAD			    0x0400
define TASK_NEW			        0x0800
define TASK_STATE_MAX			0x1000
define TASK_KILLABLE			(TASK_WAKEKILL | TASK_UNINTERRUPTIBLE)
define TASK_STOPPED			    (TASK_WAKEKILL | __TASK_STOPPED)
define TASK_TRACED			    (TASK_WAKEKILL | __TASK_TRACED)
define TASK_IDLE			    (TASK_UNINTERRUPTIBLE | TASK_NOLOAD)
define TASK_NORMAL			    (TASK_INTERRUPTIBLE | TASK_UNINTERRUPTIBLE)
define TASK_REPORT			    (TASK_RUNNING | TASK_INTERRUPTIBLE | \

{% endhighlight %}

# How to detect if the thread is idle or not?

If thread API returns 1 then it means it is idle thread.

{% highlight c %}

( ( ( item->data >> 24 ) & 0x7 ) == 1 )

{% endhighlight %}

If above condtion returns 1 then it is idle thread. For idle thread _prev_tid of sched_switch
value is 0.
