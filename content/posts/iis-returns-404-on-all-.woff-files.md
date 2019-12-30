+++
title = "IIS returns 404 on all .woff files"
date = 2014-11-10T16:32:00Z
updated = 2015-04-19T21:19:34Z
tags = ["IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

For some reason (tell me if you know why) IIS does <i>not</i>&nbsp;seem to like .woff files, and any attempt to load them for use in CSS will be met with a 404. &nbsp;I found a solution to it here, and it is to paste the following into your web.config's system.webserver section:<br /><br /><pre><code >&lt;staticContent&gt;<br />    &lt;remove fileExtension=".woff"/&gt;<br />    &lt;mimeMap fileExtension=".woff" mimeType="application/x-font-woff" /&gt;<br />&lt;/staticContent&gt;</code></pre><br />Which fixed the problem immediately!
