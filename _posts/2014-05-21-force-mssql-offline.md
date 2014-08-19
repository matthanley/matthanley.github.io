---

layout:			default
title:  		Force MS SQL Database Offline
type:			post
navigation: 	false

date:   		2014-05-21
excerpt: 		ALTER DATABASE databasename; SET OFFLINE WITH ROLLBACK IMMEDIATE
gradient: 		1
image: 			header-3.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

{% highlight sql %}
USE master
GO
ALTER DATABASE databasename
SET OFFLINE WITH ROLLBACK IMMEDIATE
GO
{% endhighlight %}
