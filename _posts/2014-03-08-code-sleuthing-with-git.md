---
category: devblog
published: true
layout: post
---

### Consider this scenario:

- You want to delete a method `foo` that seems to be no longer used.
- You're a bit nervous because you work in a dynamic language (like Ruby), so you can't rely on grep to find all usages of this method.
- You wonder, why did this method ever exist?
- `git blame` isn't very helpful - just shows the last change to that method, which isn't relevant

### git log -S to the rescue


  {% highlight console %}
    $ git log -S foo

    commit 8f19a1fa0...
    Author: Ian C. Anderson
    Date:   Thu Mar 6 21:44:17 2014 -0500

        stop using the foo method because eww

    commit 216895189...
    Author: Ian C. Anderson
    Date:   Thu Mar 6 21:09:44 1999 -0500

        new foo method - so great!
  {% endhighlight %}

From the [git-log docs](http://git-scm.com/docs/git-log):

> -S &lt;string&gt;
> Look for differences that change the number of occurrences of the
> specified string (i.e. addition/deletion) in a file.

So git will spit out all of the commits that either deleted or added the given string (e.g. calls to a method)


### Even more powerful: git log -G

> -G&lt;regex&gt;
> Look for differences whose patch text contains added/removed lines
> that match &lt;regex&gt;.

These two commands have become indispensable tools for me, especially when navigating an old codebase with a lot of crufty code.
