+++
title = "Get the maximum length of every field in a CSV, Excel etc"
date = 2019-06-30T21:15:00Z
updated = 2019-06-30T21:15:48Z
tags = ["Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

While setting up tables in our data warehouse for use with some external APIs, it was getting a little tedious to figure out the max length of some long fields to get the write size for CREATE TABLE statements, so I wrote this little script to calculate it for me. Yeah, it's kinda messy, so sue me (or don't). You can swap out the import-csv part to also import from Excel or whatever else<br /><br /><code>$csv = import-csv ~\Downloads\whatever.csv<br />$fields = $csv | select -first 1 | get-member | where MemberType -eq 'NoteProperty'<br /><br />foreach($field in $fields)<br />{<br />&nbsp; &nbsp; $data = $csv | select -ExpandProperty $field.Name<br />&nbsp; &nbsp; $lengths = $data | % {$_.Length}<br />&nbsp; &nbsp; $max = ($lengths | measure -Maximum).Maximum<br />&nbsp; &nbsp; $field | add-member -NotePropertyName MaxLength -NotePropertyValue $max<br />}<br /><br />$fields | select Name, MaxLength | Format-Table -AutoSize</code>
