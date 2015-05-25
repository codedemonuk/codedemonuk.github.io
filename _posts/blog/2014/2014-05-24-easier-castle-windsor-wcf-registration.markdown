---
layout: post
title: "Easier Castle Windsor WCF Registration"
date: 2014-05-30 14:48:00
author: Pervez Choudhury
categories: 
- Blog
- Development
- Castle Windsor
- WCF
img:
thumb: windsor-logo.png
comments: true
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

{% highlight csharp %}
public static class ContainerExtensions
{
    [SuppressMessage("Microsoft.Design", "CA1004:GenericMethodsShouldProvideTypeParameter")]
    [SuppressMessage("Microsoft.Design", "CA1026:DefaultParametersShouldNotBeUsed")]
    public static IWindsorContainer RegisterWcfService<TInterface, TConcrete>(this IWindsorContainer container, Binding binding, string name = null)
        where TInterface : class
        where TConcrete : class, TInterface
    {
      var registration = Component
        .For<TInterface>()
        .ImplementedBy<TConcrete>()
        .Named(name ?? typeof (TConcrete).Name)
        .LifestylePerWcfOperation()
        .AsWcfService(new DefaultServiceModel().Hosted().AddEndpoints(WcfEndpoint.BoundTo(binding)));
 
        return container.Register(registration);
    }
 
    [SuppressMessage("Microsoft.Design", "CA1004:GenericMethodsShouldProvideTypeParameter")]
    public static IWindsorContainer RegisterWcfExtension<TConcrete>(this IWindsorContainer container) where TConcrete : class
    {
        return container.Register(Component
                                      .For<TConcrete>()
                                      .LifestyleTransient()
                                      .Attribute("scope").Eq(WcfExtensionScope.Services));
    }
 
    [SuppressMessage("Microsoft.Design", "CA1004:GenericMethodsShouldProvideTypeParameter")]
    public static IWindsorContainer CreateWcfClient<TService>(this IWindsorContainer container, Binding binding, string endpoint) where TService : class
    {
      return container.Register(Component.For<TService>()
                                         .AsWcfClient(DefaultClientModel
                                                        .On(WcfEndpoint.BoundTo(binding)
                                                                       .At(endpoint)))
                                         .LifestyleTransient()
        );
    }
}

{%  endhighlight %}