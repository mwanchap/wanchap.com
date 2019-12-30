+++
title = "T-SQL: Easy way to check for existence of a temp table"
date = 2014-07-30T17:29:00Z
updated = 2014-07-30T17:29:00Z
tags = ["T-SQL"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Normally I'd do something like selecting from sysobjects to find if a temp table exists, but I found this little gem to drop a global temp table at the start of a query (in case it wasn't cleaned up in the previous execution):<br /><br /><code>IF(object_id('tempdb..##tmpTable') IS NOT NULL)<br /><span class="Apple-tab-span" style="white-space: pre;"> </span>DROP TABLE ##tmpTable<br />GO</code><br /><br />I'm sure you can come up with a better way to do this rather than using a global temp table, but a local one wasn't going to work in this context since I was using a combination of EXEC and OpenQuery to select from Active Directory, and regular local temp tables seem to disappear upon leaving EXEC, perhaps due to the connection changing or something?
