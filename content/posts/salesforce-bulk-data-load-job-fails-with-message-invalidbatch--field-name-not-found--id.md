+++
title = "Salesforce bulk data load job fails with message InvalidBatch : Field name not found : Id"
date = 2019-04-08T16:18:00Z
updated = 2019-04-08T16:18:02Z
tags = ["Salesforce"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

After creating a bulk / batch job, I'll sometimes see that it failed before even starting (failed batches:1, but with 0 records failed), with the following error:<br /><br />InvalidBatch : Field name not found : Id<br /><br />Annoyingly, this is caused by the inability of the Salesforce bulk import process to handle anything but ASCII.&nbsp; Try saving your CSV again, making sure it's in ASCII (called "CSV (Comma delimited)" in Excel) and not using UTF-8 or some other encoding.&nbsp; No idea how you're supposed to insert that new contact named&nbsp;José, though...
