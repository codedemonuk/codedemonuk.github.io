---
title: "Bootstrapping Psake for your windows builds"
date: 2016-06-05 15:05:00
categories:
- Psake
- Build
---

Psake is a great build system for automating your .Net builds on Windows.  To
save time when using it and to make it a simple command to run the build, I
like to place a batch file in the root of the code repository to allow you to
download and execute Psake without having to check in any binaries.

It also avoids the hassle of importing the Psake module and calling
`Invoke-Psake`

<!--more-->

{% gist codedemonuk/db3c04190e24e9870898db4f4217c763 %}