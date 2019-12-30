+++
title = "Chrome forcing all localhost queries to https, breaking various CLIs"
date = 2019-01-13T17:17:00Z
updated = 2019-01-13T20:18:05Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I use the Azure CLI and the Force.com CLI pretty regularly, and both of them make use of a little webserver running on localhost, presumably to catch the auth tokens once the SSO process redirects back. I also like to use localhost as a new tab page, to better invoke Chrome's Vimium extension on all new tabs.&nbsp; On several installs of several dev machines, http://localhost has been regularly redirected to https where it shouldn't be, causing breakage of all the CLIs, since they're not providing TLS certs, and my new tab page as I haven't got a TLS binding set up for the IIS default website.<br /><br />Today I finally figured out the fix for it, it's explained <a href="https://stackoverflow.com/a/28586593" target="_blank">here</a>, basically Chrome is forcing connections over to TLS due to a HSTS header that it's picked up for localhost.&nbsp; Deleting the security policy for the localhost domain immediately resolved all the problems I was having!&nbsp; You can get to the HSTS security policies configuration at&nbsp;<a href="chrome://net-internals/#hsts">chrome://net-internals/#hsts</a>
