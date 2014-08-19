---

layout:			default
title:  		VMware vSphere Client on Windows 8.1
type:			post
navigation: 	false

date:   		2014-05-08
excerpt: 		Installation of the VMware vSphere Client fails in Windows 8.1 due to missing .Net Framework dependencies
gradient: 		3
image: 			header-2.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

Installation of the VMware vSphere Client fails in Windows 8.1 due to missing .Net Framework dependencies. To enable, mount the Windows 8.1 ISO and run from an elevated cmd:

`Dism /online /enable-feature /featurename:NetFx3 /All /Source:D:\sources\sxs /LimitAccess`

Where D:\ is the optical drive.
