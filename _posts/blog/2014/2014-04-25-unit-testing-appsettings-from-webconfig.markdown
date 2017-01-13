---
title: "Unit testing appSettings from web.config"
date: 2010-12-22 16:54:46
categories: 
- Unit Testing
---

You can call the set method of ConfigurationManager.AppSettings to set the values required for that particular unit test.

{% highlight csharp %}
[SetUp]
public void SetUp()
{
  ConfigurationManager.AppSettings.Set("SettingKey" , "SettingValue");
  // rest of unit test code follows
}
{% endhighlight %}

When the unit test runs it will then use these values to run the code.