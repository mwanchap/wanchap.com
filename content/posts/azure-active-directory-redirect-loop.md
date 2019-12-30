+++
title = "Azure Active Directory Redirect Loop"
date = 2015-10-08T17:46:00Z
updated = 2015-10-08T17:46:18Z
tags = ["Active Directory", "Azure", "IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

While developing an Azure web app that uses Azure AD integration, I ran into a mysterious redirect loop, first on my wife's phone while trying to show it off (embarrassing!) and then again at work.  Turns out that if you don't specify https, the Microsoft sign-in page keeps redirecting back to the app and vice-versa.  Took me a little while to figure this out, thanks to <a href="https://github.com/aspnet/Security/issues/219">tugberkugurlu</a> for finding the solution!  An IIS URL Rewrite rule to force https solved the problem immediately.
