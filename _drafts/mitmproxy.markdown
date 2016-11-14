---
title:  "What's on the wire?"
description: investigating networking with mitmproxy
date: 2016-11-14
---

**Use Case**: You want to do some end-to-end testing with your app without having to rely on the backend people to flip switches.

**Approach**: If we mimick regular network behaviour we can simulate typical app scenarios.

***

### mitmproxy
When was the framework file `XYZ` *last changed* in the repository?[^1]
{% highlight Bash %}
$ pip install mitmproxy
…
Found existing installation: six 1.4.1
    DEPRECATION: Uninstalling a distutils installed project (six) has been deprecated and will be removed in a future version. This is due to the fact that uninstalling a distutils project will only partially uninstall the project.
    Uninstalling six-1.4.1:
Exception:
{% endhighlight %}


OK, so much for following instructions. -.-)

According to [this Github post|https://github.com/donnemartin/haxor-news/issues/54#issuecomment-221222383] the problem is caused by _"Apple and its included python package dependencies"_ …and we can resolve this by:

{% highlight Bash %}
$ sudo pip install mitmproxy --upgrade --ignore-installed six
{% endhighlight %}

### Setting up mitmproxy with your iPhone/iPad

A good tutorial [over here|http://jasdev.me/intercepting-ios-traffic].

***




***

### Sources

[^1]: [1. Stack Overflow][SO-last-changed]
[^2]: [2. Stack Overflow][SO-first-added]

[SO-first-added]: http://stackoverflow.com/a/25633731
[SO-last-changed]: http://stackoverflow.com/a/8611514