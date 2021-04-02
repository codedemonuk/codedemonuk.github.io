---
title: "Change the type of an AWS Parameter Store value"
date: 2021-04-02 18:00
categories:
- AWS
- PowerShell
- SSM
- Parameter Store
---

AWS Parameter Store is a great resource for storing configuation information for your applications.
It can store plain text settings as a String, as well as confidential information like passwords and connection strings as SecureString.
SecureString is encrypted by AWS when it is stored.

When setting these up, some people can go overboard and make things secure that do not need to be secure.
Normally, this is not a problem, but it is a little more inconvenient than it needs to be.

The AWS Management Console does not offer a easy way to change the type of a parameter store value once it has been created.
To do this as a one off operation, it it possible to use powershell to help you out.

## Install AWS PowerShell tools

Firstly, you will need to install the AWS PowerShell tools.
Documentation for how to [install the PowerShell tools for Windows, macOS and Linux][PowerShellToolsInstall] ia available on the AWS Documentation website.

## Approach

Using PowerShell, we will be able to read the value of the existing secure string, delete the original value, and then create a new parameter with the same name in it's place with the same value, but stored as a string.

{% gist codedemonuk/321a2f3631375cd5647111f6aff3bc3d %}

[PowerShellToolsInstall]: https://docs.aws.amazon.com/powershell/latest/userguide/pstools-getting-set-up.html