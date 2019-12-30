+++
title = "IIS and ASP.NET 404 error handlers don't play nicely together"
date = 2014-07-24T18:30:00Z
updated = 2014-07-24T18:30:39Z
tags = ["ASP.NET", "IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

While trying to setup both ASP.NET as well as IIS error-handling, I noticed that IIS wasn't dealing with certain 404 errors in which the file extension was wrong. &nbsp;For example, I could request ThisFileDoesntExist.aspx and that would redirect to NotFound.aspx just fine, but WrongExtension.aspz would kick the user out to the ugly default IIS 404 error page.<br /><br />So I did a bit of investigation and found <a href="http://forums.iis.net/t/1153365.aspx?How+to+Configure+Customer+Error+Handler+for+IIS7+for+both+static+and+dynamic+content">this</a> post, which pointed out that, in your web.config, if you have both this (relevant parts highlighted):<br /><br /><code>&lt;customErrors defaultRedirect="~/Error.aspx" mode="On" redirectMode="ResponseRedirect"&gt;<br />&nbsp; &nbsp; &lt;error statusCode="<span style="background-color: yellow;">404</span>" <span style="background-color: yellow;">redirect="~/NotFound.aspx</span>" /&gt;<br />&lt;/customErrors&gt;</code><br /><br />As well as this:<br /><br /><code>&lt;httpErrors errorMode="Custom" existingResponse="Replace"&gt;<br />&nbsp; &nbsp; &lt;remove statusCode="<span style="background-color: yellow;">404</span>" subStatusCode="-1" /&gt;<br />&nbsp; &nbsp; &lt;error statusCode="<span style="background-color: yellow;">404</span>" prefixLanguageFilePath="" path="/<span style="background-color: yellow;">NotFound.aspx</span>" responseMode="ExecuteURL" /&gt;<br />&lt;/httpErrors&gt;</code><br /><br />For some reason beyond my knowledge the IIS error handler just doesn't fire, somehow the ASP.NET 404 handling hijacks the process but doesn't get called in the event of unknown file extensions. &nbsp;However, removing the 404 element from the &lt;customErrors&gt; section lets the IIS error handling deal with every case, and all is well in my website once again. &nbsp;It makes me wonder why the customErrors section even lets you deal with 404s if it doesn't work as expected? &nbsp;But that's probably more of a gap in my knowledge than it is an issue with IIS/ASP.NET. &nbsp;Have more insight into what's going on? Let me know!
