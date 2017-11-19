---
title: "Downloading Videos from Public-i.tv"
date: 2017-11-19 23:00
categories:
- PowerShell
- Regular Expressions
---

Local Government webcasting is dominated by Public-i.
According to their website, 85% of local government bodies that stream their meetings use Public-i to do so.
They provide a good service, but one of the limitations with them is that they don't keep the videos online for too long.

If you want to watch an old video, you will need to make your own backup copy of it.
They have taken steps to ensure that it is possible to easily embed their videos onto other sites, and this work means that it is also easy to download the video itself for a given meeting.

<!--more-->

To do this, you will need to carry out a few steps.

1. Download the source to the video page
1. Parse the source for the URI of the video file
1. Extract the title from the page
1. Download the video and rename the file

This is all very easily achieved with a few lines of powershell and some regular expressions.

{% gist codedemonuk/eccc62be08581bf2683c0005cda09b2d %}
