+++
title = "Exporting from an SQL database (e.g. Dynamics) into Salesforce, without Excel"
date = 2020-01-06T17:13:00Z
updated = 2020-02-25T21:51:38Z
tags = ["Salesforce", "Powershell", "T-SQL", "Dynamics CRM 2011"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Whenever you paste content into it, Excel likes to be helpful and reformat it according to what it thinks you're doing (e.g. format dates, interpret formulae), but often with CSVs it gets this wrong and messes up your carefully-formatted raw data. This was getting pretty frustrating, so rather than figuring out workarounds for Excel's weirdness, here's how to cut out the middleman and get the output of an SQL query directly into Salesforce. Don't forget the max length variables of Invoke-SqlCmd!<br /><br /># first, write your query and save in query.sql<br />Invoke-SqlCmd -ServerInstance serverName -Database dbName -InputFile 'query.sql'&nbsp;-MaxCharLength ([Int32]::MaxValue) | Export-Csv -Path 'outputFile.csv' -Encoding ascii -NoTypeInformation<br />force login<br />force bulk -c insert -o objectName outputFile.csv<br /><br /># upsert version, won't work if you're including audit fields (CreatedDate etc)<br />force bulk -c upsert -o objectName -e External_ID__c outputFile.csv<br /><br />Invoke-SqlCmd is in the&nbsp;SqlServer module, so you'll need that first, and you'll also need the Force.com CLI installed. As a bonus, this method also removes the need to replace NULLs in the output, since they get rendered as an empty field in the CSV.
