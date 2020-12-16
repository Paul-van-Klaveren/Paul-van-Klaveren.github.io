---
title:  "When was this added/changed?"
description: Deriving the version of a manually added library that doesn't contain a version number.
date: 2015-11-20
---

**Use Case**: Your project contains a library that wasn't installed using CocoaPods or Carthage, and to make things worse, doesn't contain a version number of some sort. o.O)'

**Approach**: Assuming you always integrate the latest version of an available library, by knowing when the library was last changed you can derive what version it must be.

***

### Time to investigate
When was the framework file *last changed* in the repository?
{% highlight Bash %}
$ git log -1 --format=%cd »file«
Tue, 1 Sep 2015 12:02:22 +0200
{% endhighlight %}
(Source: [^1])

OK, now we just need to look up the latest version of the framework that would have been available on the 1st of September! 

Mystery solved.


***

### Just out of curiousity, when did we start using this library in the first place…?

When was the framework file *originally added* to the repository?
{% highlight bash %}
$ git log --diff-filter=A --follow --format=%aD -1 -- »file«
Tue Sep 29 15:47:02 2015 +0200
{% endhighlight %}
<sup>(Source: [^2])</sup> or ^this2^

***

Obviously, it would make sense to `alias` commands like these!

***

#### Sources

[^1]: [Stack Overflow][SO-last-changed]
[^2]: [Stack Overflow][SO-first-added]

[SO-first-added]: http://stackoverflow.com/a/25633731
[SO-last-changed]: http://stackoverflow.com/a/8611514