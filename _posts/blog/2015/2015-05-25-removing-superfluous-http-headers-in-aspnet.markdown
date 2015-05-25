---
title: "Removing superfluous HTTP headers in ASP.Net"
date: 2015-05-25 15:00:00
categories: 
- Blog
- Asp.net
img: aspnet-headers.png
thumb: http-protocol.png
---

When creating a new ASP.Net MVC project, by default you will end up with a number of extra HTTP headers in your responses which can safely be removed.

These headers will advertise which version of Windows you are hosting on, and which versions of the .Net framework and ASP.Net version you are developing with.  As well as being needless bloat over the wire, they are also giving away information to potential hackers about your software which can later be used to try and find vulnerabilities.

<!--more-->

The extra HTTP headers are:

    X-AspNet-Version:4.0.30319
    X-AspNetMvc-Version:5.2
    X-Powered-By:ASP.NET
    Server:Microsoft-IIS/8.0

The steps to remove each of the headers is different, but they are all very straighforward to carry out.

#### X-AspNet-Version Header

This header advertises which version if the .Net framework you are hosting on.  It's easy to remove this header because it is controlled by configuration in the `web.config` file.  Add the following configuration to remove this header.

{% highlight xml %}
<configuration>
  <system.web>
   <httpRuntime enableVersionHeader="false" />
  </system.web>
</configuration>
{% endhighlight %}

#### X-AspNetMvc-Version Header

This header advertises the version of the ASP.Net MVC framework your application was developed with.   A small code change is required to remove this header.  In your `Application_Start` method of your `Global.asax` file 

{% highlight csharp %}
MvcHandler.DisableMvcResponseHeader = true;
{% endhighlight %}

#### X-Powered-By Header

To remove this header, you need to add some extra configuration into the web.config file which is supported in IIS 7 and above.

{% highlight xml %}
<configuration>
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <remove name="X-Powered-By"/>
      </customHeaders>
    </httpProtocol>
  </system.webServer>
<configuration>
{% endhighlight %}

#### Server Header

Last, but not least is the Server header.  This effectivly advertises to hackers which version of Windows you are hosted on because IIS server versions are tied to specific releases of the Windows operating system.

There are a number of ways to remove the server header, but they involve installed components onto the web server or changing the Windows registry.  The simplest solution which will work regardless of where your application is hosted is to add the following code to your `global.asax` file.

{% highlight csharp %}
protected void Application_BeginRequest(object sender, EventArgs e)
{
    var application = sender as HttpApplication;
    if (application != null && application.Context != null)
    {
        application.Context.Response.Headers.Remove("Server");
    }
}
{% endhighlight %}