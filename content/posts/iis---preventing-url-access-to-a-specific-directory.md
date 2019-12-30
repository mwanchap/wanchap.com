+++
title = "IIS - Preventing URL Access to a Specific Directory"
date = 2014-10-09T18:08:00Z
updated = 2015-04-19T21:30:16Z
tags = ["IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Yesterday I was asked to made a web page which provided the ability to download files, which weren't served directly (by passing the file URL to the client) but were sent by reading the file on the server and sending the output. &nbsp;However, I realised that the files could still be accessed by an unauthenticated user by typing in the file's direct URL. &nbsp;Most solutions to this that I found required remote access to the server (which I don't have) or adding URL rewrite rules (the URL rewrite module wasn't installed). So I needed a solution I could implement in a web.config, and I came across the following:<br /><br /><pre><br />&lt;configuration&gt;<br />    &lt;system.webServer&gt;<br />        &lt;security&gt;<br />            &lt;requestFiltering&gt;<br />                &lt;hiddenSegments&gt;<br />                    &lt;add segment="dir_to_protect" /&gt;<br />                &lt;/hiddenSegments&gt;<br />            &lt;/requestFiltering&gt;<br />        &lt;/security&gt;<br />    &lt;/system.webServer&gt;<br />&lt;/configuration&gt;<br /></pre><br />Works like a charm! The file download code still works (since it's just reading the files directly) , and any attempt to access the files via their URLs returns a 404.
