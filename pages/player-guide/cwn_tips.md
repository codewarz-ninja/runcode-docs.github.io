---
title: Tips
keywords: codewarz
summary: "Various tips and miscellaneous information."
sidebar: cwn_sidebar
permalink: cwn_tips.html
folder: player-guide
---

## Flag Format

Several of the challenges will have you perform some action and then print a 'flag' to prove that you have completed said actions. The format for the flags (so that you know it when you see it) is:
{% highlight text %}
CWN{a-zA-Z0-9_-!?&$%^#@}
{% endhighlight %}

Some of the older challenges may still use the older prefix and appear as such:
{% highlight text %}
CTD{a-zA-Z0-9_-!?&$%^#@}
{% endhighlight %}
Yes, flags for the backend are different than what you see on the test servers/sockets so just printing what you got for the test server won't work on the backend.

## Notes on scapy (python module)
Scapy is a very powerful tool. For our usage here, you generally should only ever need to read packet captures and should not have the need to send anything over the wire. The user your code will run as lacks the permissions to do such, anyways. Maybe at a later competition we might implement a challenge or two that would need to do this. For now, you should be fine without being able to craft packets to be sent over the wire.

Scapy likes to whine and cry when it doesn't see an IPv6 interface when you fire it up. This could very likely cause you great pain on a few of your solves. We suggest taking advantage of the built-in logging functions to do something like, say, only have it print actual errors instead of warnings or whatever. Here's an example of how to handle this:

{% highlight python %}
import logging
logging.getLogger("scapy.runtime").setLevel(logging.ERROR)
from scapy.all import *
{% endhighlight %}

## What's in a name?

So, we did a total rewrite on the codebase, in off-hours from work, over the past few months. This rewrite is what you see in front of you, now. From a user perspective, not much has really changed except maybe better UX for stuff like messages from the server. Anyways, it needed a name, so for now, it's Curmudgeon.

>a bad-tempered or surly person.

Seems fitting, I think! Hope you like it.



{% include links.html %}
