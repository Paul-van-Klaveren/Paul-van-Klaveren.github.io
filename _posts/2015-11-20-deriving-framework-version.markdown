---
title:  "When was this added/changed?"
description: Deriving the version of a manually added library that doesn't contain a version number.
date: 2015-11-20
---

**Use Case**: Your project contains a library that wasn't installed using CocoaPods or Carthage, and to make things worse, doesn't contain a version number of some sort. o.O)'

**Approach**: Assuming you always integrate the latest version of an available library, by knowing when the library was last changed you can derive what version it must be.

***

### Time to investigate
When was the framework file `xyz` *last changed* in the repository?[^1]
{% highlight Bash %}
$ git log -1 --format=%cd xyz
# Tue, 1 Sep 2015 12:02:22 +0200
{% endhighlight %}

OK, now we just need to look up the latest version of the framework that would have been available on the 1<sup>st</sup> of September! 

Mystery solved.


***

### Just out of curiousity, when did we start using this library in the first place…?

When was the framework file *originally added* to the repository? [^2]
{% highlight bash %}
$ git log --diff-filter=A --follow --format=%aD -1 -- xyz
# Tue Sep 29 15:47:02 2015 +0200
{% endhighlight %}

***

Obviously, it would make sense to `alias` hard-to-remember commands like these!

***

### Sources

[^1]: [1. Stack Overflow][SO-last-changed]
[^2]: [2. Stack Overflow][SO-first-added]

[SO-first-added]: http://stackoverflow.com/a/25633731
[SO-last-changed]: http://stackoverflow.com/a/8611514