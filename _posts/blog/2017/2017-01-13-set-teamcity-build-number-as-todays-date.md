---
title: "Set TeamCity's build number a todays date"
date: 2017-01-13 17:00
categories: 
- TeamCity
---

When using TeamCity to run daily builds for things like unit test coverage,
duplicate code, security auditing, which can be time consuming running as part
of every commit, it is handy to be able to see which date they were run.

This can be easily achived by setting the TeamCity build number as the date
the build was started.

Add a Powershell build step to the build with the following code definition

{% gist codedemonuk/761bffc2d51b162ebc35 %}
