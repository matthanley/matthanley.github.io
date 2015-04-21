---

layout:			default
title:  		SQL Server - Get total size of all DBs
type:			post
navigation:     false

date:   		2015-04-21
excerpt: 		
gradient: 	    3
image: 			header-4.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

# MS SQL Server

Get total size of all databases on an instance:

```
SELECT CONVERT(DECIMAL(10,2),(SUM(size * 8.00) / 1024.00 / 1024.00)) As UsedSpace
FROM master.sys.master_files
```
