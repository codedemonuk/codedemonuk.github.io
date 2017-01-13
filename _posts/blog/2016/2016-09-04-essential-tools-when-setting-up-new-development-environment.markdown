---
title: "Essential tools when setting up a new development environment"
date: 2016-09-04 18:50:00
categories:
- Tools
- Development
---

A list of essentials tools when setting up a new machine for software development.

<!--more-->

## Terminals

* [ConEmu](https://conemu.github.io/en/)  
  `choco install conemu`

* [PowerShell 5](https://www.microsoft.com/en-us/download/details.aspx?id=50395)  
  `choco install powershell`

## IDE

* [Visual Studio Community]()  
  `choco install visualstudio2015community`

* [Visual Studio Code](https://code.visualstudio.com/)  
  `choco install visualstudiocode`

## IDE Extensions

### Visual Studio
* Resharper
* DotTrace
* Web Essentials

### Visual Studo Code
* PowerShell
* C#

## Languages

* Node (via NVM)
* [Go](https://golang.org/)  
  `choco install golang`
* [.NET Core](https://www.microsoft.com/net/core)
* [.Net Framework 4.6.2](https://www.microsoft.com/net/download)  
  `choco install dotnet4.6.2`

## .NET development tools

* [DotPeek](https://www.jetbrains.com/decompiler)  
  Decompile .NET assemblies to C# using JetBrains Resharper build in decompiler.  
  `choco install dotpeek`
* [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)  
  NuGet Package Explorer is a ClickOnce application which allows creating and exploring NuGet packages easily. After installing it, you can double click on a .nupkg file to view the package content. You can also load packages directly from the official NuGet feed.  
  `choco install nugetpackageexplorer`
* [FxCop](https://fxcopinstaller.codeplex.com/)  
  FxCop is an application that analyzes managed code assemblies (code that targets the .NET Framework common language runtime) and reports information about the assemblies, such as possible design, localization, performance, and security improvements.  
  `choco install fxcop`

## HTTP Development
* [Fiddler](http://www.telerik.com/fiddler)  
  `choco install fiddler`
* [Postman](https://www.getpostman.com/)  
  `choco install postman`

## Browsers

* [Firefox Developer Edition](https://www.mozilla.org/en-GB/firefox/developer/)  
* [Chrome](https://www.google.com/chrome)  
  `choco install googlechrome`

## Installers

* Chocolatey    
  `@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`

## Source Control

* SourceTree  
  `choco install sourcetree`
* TortoiseGit  
  `choco install tortoisegit`
* [PoSH Git]()  
  `choco install poshgit`   
* [Git Command Line](https://git-scm.com/downloads)  
  `choco install git`
* Git Credential Manager for Windows  
  `choco install git-credential-manager-for-windows`

## Merge

* [KDiff3](http://kdiff3.sourceforge.net/)  
  Very good open source 3 way merge and diff tool.  
  `choco install kdiff3`

# Virtual Machines

* [Docker](https://www.docker.com/)  
  An open platform for developers and sysadmins to build, ship, and run distributed applications.  
  `choco install docker`

## Data

* [LinqPad](https://www.linqpad.net)  
  `choco install linqpad`
* [Redis for Windows](https://github.com/MSOpenTech/redis)  
  `choco install redis-64`
* [SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/mt238290.aspx)  
  `choco install mssqlservermanagementstudio2014express`
* [Redis Desktop Manager](https://redisdesktop.com/)    
  A fast open source Redis database management application.    
  `choco install redis-desktop-manager`   

## Misc

* [Baretail](https://www.baremetalsoft.com/baretail)  
  A free real-time log file monitoring tool.  
  `choco install baretail`
* [Slack](https://slack.com/is)  
  `choco install slack`