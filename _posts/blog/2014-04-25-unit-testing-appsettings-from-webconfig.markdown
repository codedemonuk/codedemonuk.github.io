---
layout: post
title: "Unit testing appSettings from web.config"
date: 2010-12-22 16:54:46
author: Pervez Choudhury
categories: 
- Blog
- Development
- Unit Testing
img: php_code.png
thumb: php_code.png
---

You can call the set method of ConfigurationManager.AppSettings to set the values required for that particular unit test.

    [SetUp]
    public void SetUp()
    {
      ConfigurationManager.AppSettings.Set("SettingKey" , "SettingValue");
      // rest of unit test code follows
    }

When the unit test runs it will then use these values to run the code

[hampden]: https://github.com/jekyll/jekyll