---
title: "Auto reconnecting Margiebot to Slack"
date: 2016-06-05 12:30:00
categories:
- Slack
- MargieBot
---

[MargieBot][1] is a simple to use .Net framework for making your own bots for
Slack.  To start up a bot and connect it to Slack, all it takes is:

{% highlight csharp %}
Bot myBot = new Bot();
myBot.Connect("<your bot's slack API token>");
{% endhighlight %}

This makes the happy path work very well, but out of the box this will not
handle dropped connections or attempting to reconnect to the server - so if the
connection is interrupted for any reason, you bot will no longer try to connect
to Slack.

<!--more-->

Fortunately MargieBot offers an extensibility point that we can use to add this
functionality in.  

MargieBot emits a `ConnectionStatusChanged` event when the bot connects or
disconnects from Slack.  it also exposes a public property called `IsConnected`.

We can wire up an event handler to the `ConnectionStatusChanged` event like so:

{% highlight csharp %}
_bot = new Bot();
_bot.ConnectionStatusChanged += ConnectToSlackIfDisconnected;
{% endhighlight %}

Our event handler can then try to establish a connection to Slack and retry
until it is able to do so.

{% gist codedemonuk/2bc8d60fc2ea370a75ccb4abbba5578e %}

We can also re-ue this code when making the initial connection to Slack. Instead
 of calling
{% highlight csharp %}
_bot.Connect("<Slack API Token>") // do not do this anymore
{% endhighlight %}
 you can call the event handler explicitly with:

{% highlight csharp %}
ConnectToSlackIfDisconnected(false); // do this instead!
{% endhighlight %}

[1]: https://github.com/jammerware/margiebot
