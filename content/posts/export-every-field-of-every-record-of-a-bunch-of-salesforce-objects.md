+++
title = "Export every field of every record of a bunch of Salesforce objects"
date = 2020-03-04T17:56:00Z
updated = 2020-03-04T17:56:18Z
tags = ["Salesforce", "Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I needed to get a backup of every record of a bunch of objects (for posterity) which were about to be deleted, I wanted to grab every field and do it in one line. I cheated a little, because I've defined some functions that just do some of the basic processing. I could put the whole function definitions on one line too, but that'd be a bit contrived ;) They're below for reference<br /><br /><br /><div><br /></div><pre>('object_name_1__c','object_name_2__c') |<br />foreach-object {<br />    $fields = (sffields $_) -join ','<br />    $query = "select $fields from $_"<br />    sfquery $query | export-csv "$_.csv" -NoTypeInformation -Encoding ASCII<br />}<br /><br />function SFFields<br />{<br />    (force describe -n="$($args[0])" -t=sobject | ConvertFrom-Json).Fields | Sort-Object name | Select-Object -ExpandProperty name<br />}<br /><br />function SFQuery<br />{<br />    force query --format json $args[0] | ConvertFrom-Json<br />}<br /></pre>
