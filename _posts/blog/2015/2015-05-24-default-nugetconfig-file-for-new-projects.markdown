---
title: "Default nuget.config file for new projects"
date: 2015-05-24 14:48:00
categories: 
- NuGet
---

When starting a new .Net project, I like to place a nuget.config in the solution root folder with a number of default settings in place.  This is to ensure a number of good behaviours for NuGet.

<!--more-->

* Allow Package Restore
* Add the public NuGet repository and any organisational NuGet repositories
* Ensure all NuGet packages are saved in a common `packages` folder

{% gist codedemonuk/74b4e55276c8de4f63f0 %}