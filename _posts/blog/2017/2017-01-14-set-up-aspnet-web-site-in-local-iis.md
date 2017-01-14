---
title: "Set up an ASP.Net web site in your local IIS"
date: 2017-01-14 15:50
categories: 
- IIS
- ASP.Net
---

When working on an ASP.net application, it can be very useful to be able to
quickly set up the project in your local IIS server so you can build it and
start using it.

I have a couple of scripts that I like to drop into the root of my ASP.net
repositories which will quickly set up IIS for your project.

<!--more-->

## Install Website

This script will set up IIS, application pools, binding and local host file
entries for your website.

{% gist codedemonuk/f2e8a5b0a25f78c965ba24ff81646060 %}

## Uninstall Website

This script will undo all of the good work carried out by the install script.

{% gist codedemonuk/29a2085855c82ffacb8dfd9dbe68e2b0 %}