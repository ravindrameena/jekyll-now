---
layout: post
title: POSIX Compliance (Getting started challenge for RTEMS beginners) 
---

POSIX stands for Portable Operating System Interface for uni-X. POSIX Compliance allows us to 
port the source code that is running on one machine, can be run on another machine. This 
Project deals with the implementation of a subset of functions that are defined in POSIX 
1003_1 standard, Due to physical resource constraints, some real-time systems like the small 
embedded system needs a limited set of operating system functionality. For these type of 
system, it is necessary that the standards allow the implementation to support only a 
particular subset of POSIX functions. Real-Time Working Group addressed this subset of 
function.POSIX profiles defined in FACE Technical Standards, designed for avionics system 
versus POSIX in RTEMS where some functions are missing.

RTEMS Initial Setup:

**Step 1:** Install prerequisites 

{% highlight c %}

$ sudo apt-get install build-essential
$ sudo apt-get build-dep binutils gcc g++ gdb unzip git python2.7-dev
$ sudo apt-get install git

{% endhighlight %}

**Step 2:** RTEMS prefix and setting path

{% highlight c %}

$ export PATH=$HOME/development/rtems/5/bin:$PATH

{% endhighlight %}

**Step 3:** RTEMS setup

{% highlight c %}

$ mkdir development/rtems/src
$ cd development/rtems/src

{% endhighlight %}
2019-06-15-Fourth-Post
**Step 4:** Clone RTEMS Source Builder git repository (within the src directory):-

{% highlight c %}

$ git clone git://git.rtems.org/rtems-source-builder.git
$ cd rtems-source-builder

{% endhighlight %}

**Step 5:** Now we check whether the host is setup correctly or not using this command:-

{% highlight c %}

$ source-builder/sb-check

{% endhighlight %}

If this message appeared in the terminal that means the host is set up correctly.

“RTEMS Source Builder environment is ok.”

**Step 6:** To check the list of architectures, supported by RTEMS

{% highlight c %}

$ ./source-builder/sb-set-builder –list-bsets

{% endhighlight %}

**Step 7:** For SPARC architecture :

{% highlight c %}

$ cd rtems
$ ../source-builder/sb-set-builder --log=l-sparc.txt --prefix=$HOME/development/rtems/5 5/rtems-sparc

{% endhighlight %}

Note : If Building process is failed, then go to the directory 
/develeopment/rtems/src/rtems-source-builder/rtems and check the reason in log file 
sparc.txt file.

This command download, build and install the tool chain here :

$HOME/development/rtems/5

**Step 7:** Now environment for SPARC is set up. We need to download rtems5.

{% highlight c %}

$ cd
$ cd development/
$ git clone git://git.rtems.org/rtems rtems5
$ ls $HOME/development/rtems/5/bin

{% endhighlight %}

**Step 8:** Configuring and compiling RTEMS5:-

{% highlight c %}

$ cd rtems5
$ export PATH=$HOME/development/rtems/5/bin:$PATH
$ ./bootstrap
$ cd ..
$ sudo rm -r b-sparc
$ mkdir b-sparc
$ cd b-sparc
$ ../rtems5/configure --target=sparc-rtems5 –enable-rtemsbsp=erc32 --enable-tests=samples \ 
--enable-posix
$ make
$ sudo PATH=$HOME/development/rtems/5/bin:$PATH make install

{% endhighlight %}

**Step 9:** To check whether the hello world.exe is generated or not, try this command :-

{% highlight c %}

$ cd development/b-sparc

$ sparc-rtems5-gdb `find . -name ticker.exe`

{% endhighlight %}

Here, we can use path of .exe file within the testsuites instead of find command. I had 
modified the ticker application.

To modify any tests, one needs to go to the samples directory located at $HOME/
development/rtems5/testsuites/samples/

Go to any specific application directory and change the code.

After adding code or modifying any file, you need to run make and make install(use sudo with PATH)
commands.

Above command find the hello.exe file.

$ tar sim

$ load

$ r

Done :) Send the output and patch on devel@rtems.org