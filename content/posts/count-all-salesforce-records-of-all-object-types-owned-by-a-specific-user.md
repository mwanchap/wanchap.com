+++
title = "Count all Salesforce records of all object types owned by a specific user"
date = 2019-12-12T21:56:00Z
updated = 2019-12-12T21:56:33Z
tags = ["Salesforce", "Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

It's not the fastest or most elegant script, but using the Force.com CLI it's pretty easy to get a count of objects (of all types) owned by a specific user. It assumes that the field to be checked is ownerid, though, so might not work if you have other fields. A slightly better way might be to check which objects have an ownerid field first.<br /><br /><pre>$ErrorActionPreference = 'SilentlyContinue'<br />$objects = force sobject list<br />$ownerId = '00590000001Abcd' # obviously replace this<br /><br />foreach($object in $objects)<br />{<br />    $resp = (force query --format json "select count(id) from $object where ownerid='$ownerId'" | convertfrom-json | select -ExpandProperty expr0)<br />    $count = 0<br />    if([Int32]::TryParse($resp, [ref]$count) -and $count -gt 0)<br />    {<br />        "$object : $count"<br />    }<br />}<br /></pre>
