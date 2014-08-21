---

layout:			default
title:  		Hide Pinned Taskbar Icons for RDS Server
type:			post
navigation: 	false

date:   		2014-05-21
excerpt: 		Remove pinned taskbar icons via local Group Policy
gradient: 		4
image: 			header-4.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

1. Run `gpedit.msc` to access the Local Group Policy Editor on the Server
2. Navigate to `User Configuration\Administrative Templates\Start Menu and Taskbar`
3. Enable the setting `Remove pinned programs from the Taskbar`
