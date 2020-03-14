+++
title = "One-liner to check/uncheck every checkbox on a page"
date = 2020-03-12T17:53:00Z
updated = 2020-03-12T17:53:03Z
tags = ["Javascript"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Press F12, click console and paste this in there. <br /><code>[].slice.call(document.querySelectorAll("input")).forEach(i =&gt; i.checked=true) </code>
