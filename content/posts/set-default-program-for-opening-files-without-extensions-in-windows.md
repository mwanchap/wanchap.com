+++
title = "Set default program for opening files without extensions in Windows"
date = 2019-10-29T23:41:00Z
updated = 2019-10-29T23:41:04Z
tags = ["Salesforce"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

For some reason, downloading the request / result CSV files for a Salesforce "Bulk Data Load" job returns CSV files with the file extension missing, so you can't just click to open them. This became super annoying during a troublesome data load so I decided to fix it once and for all.&nbsp; Open cmd as admin and enter the following:<br /><br /><pre>assoc .="No Extension"<br />ftype "No Extension"="C:\ProgramData\chocolatey\lib\csvfileview\tools\CSVFileView.exe" "%1"</pre><br /><br />Obviously substitute in your favourite CSV editor (unless by some bizarre coincidence, you also like CSVFileView and install everything with chocolatey).&nbsp; Credit for the solution goes to <a href="https://superuser.com/a/13947/1020545" target="_blank">this post</a> on superuser.
