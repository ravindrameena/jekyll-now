---
layout: post
title: Useful Git commands 
---

This post will guide you through usefull Git commands.

**1.** To install Git

{% highlight c %}

sudo apt-get install git

{% endhighlight %}

**2.** Initialise Git repository.

{% highlight c %}

git init

{% endhighlight %}

**3.** To show the status of Git repository. It show the list of files and created directory where we made our changes

{% highlight c %}

git status

{% endhighlight %}

**4.** To know the latest commits in master repository

{% highlight c %}

git log

{% endhighlight %}

**5.** To know the current working branch

{% highlight c %}

git branch

{% endhighlight %}

**6.** To make a switch on other existing branch

{% highlight c %}

git checkout BRANCH_NAME

{% endhighlight %}

**7.** To create a new branch

{% highlight c %}

git checkout -b BRANCH_NAME

{% endhighlight %}

**8.** To add new file

{% highlight c %}

git add .LOCATION_OF_FILE 

{% endhighlight %}

**9.** To commit locally with message.

{% highlight c %}

git commit -m “Title of patch”

{% endhighlight %}

**10.** To generate patch file. Here i = No. of patches you want to generate.

{% highlight c %}

git format-patch BRANCH_NAME~i

{% endhighlight %}

**11.** To generate next version of patch.

{% highlight c %}

git format-patch BRANCH_NAME~i -vn

{% endhighlight %}

**12.** To send email

{% highlight c %}

sudo apt-get install git-email // Installs the git email
git send-email LOCATION_OF_PATCH_FILE --to=devel@rtems.org --cc=_EMAIL_ID //to send a email

{% endhighlight %}

**13.** To apply a patch

{% highlight c %}

git am LOCATION_OF_PATCH

{% endhighlight %}

**14.** To rebase

{% highlight c %}

git rebase -i HEAD~n //Here, n=1,2,..N which tells number of commits you would like to edit

{% endhighlight %}
