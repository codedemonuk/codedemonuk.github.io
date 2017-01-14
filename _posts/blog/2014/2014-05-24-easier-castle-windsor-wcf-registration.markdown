---
title: "Easier Castle Windsor WCF Registration"
date: 2014-05-30 14:48:00
categories: 
- Inversion of Control
- WCF
---

Castle Windsor has a great add on called the [WCF Integration Facility](https://www.nuget.org/packages/Castle.WcfIntegrationFacility/) which allows you to get all of the benefits of DI/IoC when working with WCF services.

The only downside of using it is the verbosity of the component registration.  Thankfully we are able to use extension methods to help us here and hide away all of the verbose registration code behind a simple, chainable method call.

<!--more-->

#### Register a WCF Service

Using an extension method, you can register a WCF service very simply and easily. 

{% highlight csharp %}
var netTcpBinding = new NetTcpBinding();
container.RegisterWcfService<IMyService, MyConcreteService>(netTcpBinding);
{% endhighlight %}

#### Register a WCF Client

WCF client registration also becomes very simple as well.

{% highlight csharp %}
var httpBinding = new HttpBinding();
container.RegisterWcfClient<IMyService>(httpBinding, "http://your-url/service.svc");
{% endhighlight %}

#### The extension methods

These extension methods also return the `IWindsorContainer` intance allowing multiple registrations to be chained in a fluent manner.

{% gist codedemonuk/4458c6386157a7c159d1 %}