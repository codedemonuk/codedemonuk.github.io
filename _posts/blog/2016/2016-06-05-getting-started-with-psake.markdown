---
title: "Bootstrapping Psake for your windows builds"
date: 2016-06-05 15:05:00
categories:
- Blog
- Psake
- Build
img:
thumb: php_code.png
---

Psake is a great build system for automating your .Net builds on Windows.  To
save time when using it and to make it a simple command to run the build, I
like to place a batch file in the root of the code repository to allow you to
download and execute Psake without having to check in any binaries.

It also avoids the hassle of importing the Psake module and calling
`Invoke-Psake`

<!--more-->

{% highlight batch %}

	@echo off

	:: Download NuGet
	if not exist ".\build\tools" mkdir ".\build\tools"
	if not exist ".\build\tools\nuget" mkdir ".\build\tools\nuget"
	if not exist ".\build\tools\nuget\nuget.exe" powershell -Command "Invoke-WebRequest https://www.nuget.org/nuget.exe -OutFile .\build\tools\nuget\nuget.exe"

	:: Download Psake
	set nuget=.\build\tools\nuget\nuget.exe
	set EnableNuGetPackageRestore=true

	%nuget% install psake -ExcludeVersion -NonInteractive -OutputDirectory ".\build\tools" -Verbosity quiet

	call .\build\tools\psake\tools\psake.cmd .\build\build.ps1 %*

{% endhighlight %}
