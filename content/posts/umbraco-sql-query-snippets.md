+++
title = "Umbraco SQL query snippets"
date = 2019-12-10T22:32:00Z
updated = 2019-12-10T22:32:13Z
tags = ["Umbraco", "T-SQL"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Selecting properties of a content item:<br /><br />SELECT&nbsp; cast([xml] as xml) as 'xmldata', nodeId<br />FROM&nbsp; &nbsp; dbo.cmsContentXml<br />WHERE&nbsp; &nbsp;nodeId = '1234' --ID from the node in Umbraco<br /><div><br /></div><div><br /></div>
