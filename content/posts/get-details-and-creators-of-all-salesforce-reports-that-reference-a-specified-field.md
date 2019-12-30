+++
title = "Get details and creators of all Salesforce reports that reference a specified field"
date = 2019-04-09T15:08:00Z
updated = 2019-04-09T15:08:41Z
tags = ["Salesforce", "Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

If you're ever modifying a Salesforce field and you want to contact everyone who has created reports using the field, here's how you do that using Powershell and the <a href="https://force-cli.heroku.com/" target="_blank">Force.com CLI</a>&nbsp;(which you can also install via <a href="https://chocolatey.org/packages/force-cli" target="_blank">chocolatey</a>):<br /><br />set-location C:\wherever<br />force export<br />$reportFiles = get-childitem&nbsp;-Path .\src\reports\ -Recurse | sls "field_to_search_for"<br /><br /># I've included some extra fields here, they might come in useful<br />$reportData = force query --format=json "select id, createdby.name, createdby.email, developername, name, foldername, isdeleted, lastrundate, lastvieweddate from report" | convertfrom-json<br />$matchingReports = $reportData | where { $reportFiles.Filename -eq $_.DeveloperName + ".report" }<br /><br />$matchingReports | % { $_.createdby.name + ' created report "' + $_.name +'"' }<br /># send an email to these folks: $matchingReports.Createdby.email | select -Unique
