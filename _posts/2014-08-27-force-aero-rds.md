---

layout:			default
title:  		Force Aero theme for RDS Server
type:			post
navigation: 	false

date:   		2014-08-27
excerpt: 		Provide Windows 7 Aero experience to remote users via local Group Policy
gradient: 		4
image: 			header-2.jpg
details:		false

author: 		Matt Hanley
bio: 			"Yup, <i>that</i> guy."
twitter: 		"https://twitter.com/_matthanley"

---

0. Install `Remote Desktop Session Host` _role_ and `Desktop Experience` _feature_
1. Run `gpedit.msc` to access the Local Group Policy Editor on the Server
2. Navigate to `User Configuration\Administrative Templates\Control Panel\Personalization`
3. Enable the setting `Force a specific visual style file or force Windows Classic` with value `%windir%\resources\themes\aero\aero.msstyles`
4. Enable the setting `Load a specific theme` with value `%windir%\resources\themes\aero.theme`
