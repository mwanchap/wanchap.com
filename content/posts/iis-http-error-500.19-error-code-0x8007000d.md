+++
title = "IIS HTTP Error 500.19, Error Code 0x8007000d"
date = 2018-01-19T18:27:00Z
updated = 2018-01-19T18:29:45Z
tags = ["IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I probably come across this error at least once per year. Ran into it again today when setting up a website to host locally in IIS, on a computer I don't use much.<br /><br /><code>HTTP Error 500.19 - Internal Server Error<br />The requested page cannot be accessed because the related configuration data for the page is invalid.<br /><br />Detailed Error Information:<br />Module<span style="white-space: pre;"> </span>&nbsp; &nbsp;IIS Web Core<br />Notification<span style="white-space: pre;"> </span>&nbsp; &nbsp;Unknown<br />Handler<span style="white-space: pre;"> </span>&nbsp; &nbsp;Not yet determined<br />Error Code<span style="white-space: pre;"> </span>&nbsp; &nbsp;0x8007000d<br /><br />Config Source:<br />&nbsp; &nbsp;-1:<br />&nbsp; &nbsp; 0:<br /></code><br /><div><br /></div>Microsoft's documentation for that error code helpfully points out:<br /><br /><i>"This problem occurs because the ApplicationHost.config file or the Web.config file contains a malformed XML element."</i><br /><br />Well that clears it up. Just remove the malformed XML element on line 0...<br /><br />Except that the site runs just fine on other systems, and even in IIS Express on the same machine that's causing the error, so clearly there's no "malformed XML".&nbsp; Anyway, it turns out that if your web.config has a section for something like IIS' URL Rewrite module, but you don't have it installed, IIS will get <b>so mad&nbsp;</b>that all you'll deserve is the silent scorn of an empty error message.<br /><br />In my case, the solution was to install the URL Rewrite module via the web platform installer.
