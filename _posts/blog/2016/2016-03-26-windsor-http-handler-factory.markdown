---
title: "Castle Windsor ASP.Net HTTP Handler Factory"
date: 2016-03-26 15:30:00
categories:
- Castle Windsor
---

When writing a simple HTTP handler in .Net, the framework provides support for
replacing the default HTTP Handler Factory with your own factory which provides
support for dependency injection.

<!--more-->

The framework exposes an interface called `IHttpHandlerFactory` which you will
need to implement with the code for your custom factory.

## The HTTP Handler Factory

Here's one I prepared earlier that will return HTTP handlers based on the name
the classed were registered with in Castle Windsor.

{% gist codedemonuk/46cfbaa079e10ed14d69c684eab10c2e %}

It makes the assumption that your `HttpApplication` class in `Global.asax.cs`
exposes the container, via the IContainerAccessor interface.

## Wiring it in

You will need to add an entry in your `web.config` file that tells the framework
to use your factory to satisfy HTTP requests.

{% highlight xml %}

<configuration>
	<system.webServer>
		<handlers>
			<add
				verb="GET,POST"
				path="*.sample"
				name="HandlerFactory"
				type="CastleWindsorHttpHandlerFactory"/>
		</handlers>
  </system.webServer>
</configuration>

{% endhighlight %}

This will register the extension .sample to have it's requests satisfied by the
class that Castle Windsor believes is appropriate to handle that request
based on the logic in your handler factory.

More details for how to do this can be found on the [MSDN article on creating
and registering HTTP handler factories][1]

[1]: https://msdn.microsoft.com/en-us/library/aa720140(v=vs.71).aspx
