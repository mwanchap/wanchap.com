+++
title = "String.LastIndexOf, but in T-SQL (handy for getting file extensions)"
date = 2020-03-09T17:12:00Z
updated = 2020-03-09T17:12:14Z
tags = ["T-SQL"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Note that this doesn't work on the "text" datatype, so you'll need to cast to nvarchar...  <pre><br />SELECT  LEN(FileName) - CHARINDEX('.', REVERSE(FileName)) AS 'LastIndex',<br />        RIGHT(FileName, CHARINDEX('.', REVERSE(FileName))) AS 'FileExtension' -- still includes the dot<br />FROM    Files<br /></pre>
