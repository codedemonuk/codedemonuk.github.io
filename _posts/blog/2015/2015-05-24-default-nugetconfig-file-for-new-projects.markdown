---
title: "Default nuget.config file for new projects"
date: 2015-05-24 14:48:00
categories: 
- Blog
- Development
- NuGet
img: nuget-stickers.jpg
thumb: nuget.png
---

When starting a new .Net project, I like to place a nuget.config in the solution root folder with a number of default settings in place.  This is to ensure a number of good behaviours for NuGet.

<!--more-->

* Allow Package Restore
* Add the public NuGet repository and any organisational NuGet repositories
* Ensure all NuGet packages are saved in a common `packages` folder

{% highlight xml %}

<?xml version="1.0" encoding="utf-8"?>
<configuration>

    <config>
        <add key="repositorypath" value=".\Packages" />
    </config>

    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>

    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="Public Nuget Server" value="https://nuget.org/api/v2/"/>
        <!-- Add any other internal corporate package sources here -->
    </packageSources>

    <activePackageSource>
        <add key="All" value="(Aggregate source)" />
    </activePackageSource>

</configuration>

{% endhighlight %}