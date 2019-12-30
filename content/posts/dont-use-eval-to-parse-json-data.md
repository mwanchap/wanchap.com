+++
title = "Don't use eval to parse JSON data"
date = 2014-05-20T22:26:00Z
updated = 2014-05-20T22:26:14Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Today I read about an interesting security vulnerability in Javascript's eval() function that I wasn't aware of previously (which I was naively using to parse JSON data). &nbsp;Open a developer console and try this:<br /><br /><div style="text-align: center;"><code>eval("alert('pwned')")</code></div><br />The code is executed! This could perhaps be used to return malformed instructions instead of JSON and do something malicious to the client. &nbsp;However, try this:<br /><br /><div style="text-align: center;"><code>JSON.parse("alert('not pwned')")</code></div><br />Notice that it just throws a parsing error, but of course for actual JSON it still produces the correct object. &nbsp;Also, here's a <a href="http://stackoverflow.com/a/198031">relevant stackoverflow answer</a>.
