+++
title = "Powershell jobs"
date = 2018-12-12T00:19:00Z
updated = 2019-06-23T17:25:01Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Mostly for my own benefit but maybe someone will find this a helpful and concise reference<br /><br />Create a job like this<br />$job = start-job {sleep 60; get-service;}<br /><br />If you're creating jobs in a loop, add them to an array<br />$jobs = @()<br />foreach ($asdf in $qwer) { $jobs += start-job {...} }<br /><br />Check job status while a job is running with<br />$job | get-job<br /><br />Receive the result of that job with<br />$jobResult = ($job | wait-job | receive-job)<br /><br /><h4>To execute some command over a large number of servers:</h4>$creds = get-credential<br /><br />$scriptBlock = {<br />Param($server,$creds)<br />&nbsp; &nbsp; write "running on $server";<br />&nbsp; &nbsp; Invoke-Command -ComputerName $server -Credential $creds -Command {<br />&nbsp; &nbsp; &nbsp; &nbsp; &amp; {get-childitem -Path 'C:\' -Filter 'whatever' -Recurse } 2&gt;$null 3&gt;$null<br />&nbsp; &nbsp; }<br />}<br /><br />$servers = @("server1", "server2", "server3", "etc")<br />$servers | % {<br />&nbsp; &nbsp; start-job -ScriptBlock $scriptBlock -ArgumentList $_,$creds<br />}
