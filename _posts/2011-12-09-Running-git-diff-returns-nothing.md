---
layout: post
title: Running 'git diff' returns nothing
---

I was surprised when I ran a 'git diff' command and it returned nothing.

{% highlight bash %}
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file:   404.html
#   modified:   _layouts/default.html
#   modified:   atom.xml
#   modified:   index.html
$ git diff
{% endhighlight %}

Coming from a background of using Mercurial, this kind of confused me.

The default output for git diff is the list of changes which have not been committed/added to the index. If there are no changes, then there is no output.

In my case I had already run a 'git add' so my changes were 'staged'.

In this case, just run either of these commands:

{% highlight bash %}
git diff HEAD
git diff --cached
{% endhighlight %}

Based off answers from "here.":http://stackoverflow.com/questions/3580608/git-diff-does-nothing
