+++
title = "Powershell as a Visual Studio External Tool"
date = 2017-10-22T18:12:00Z
updated = 2017-10-22T18:12:39Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

It's handy to be able to open Powershell at the current solution directory, e.g. for invoking scripts or git commands etc.<br />Click the Tools menu&nbsp; -&gt; External Tools -&gt; Add<br />Title: Powershell, or whatever you want<br />Command: your PS directory, e.g C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe<br />Arguments:&nbsp;-ExecutionPolicy RemoteSigned -NoExit -Command "Set-Location '$(SolutionDir)' | Clear-Host"<br />Initial directory:&nbsp;$(SolutionDir)
