+++
title = "Powershell - normalizing line endings for all files in a directory"
date = 2019-10-22T23:32:00Z
updated = 2019-11-04T17:44:00Z
tags = ["Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

If you're working with a git repository, a much better way to solve this is by changing the&nbsp;core.autocrlf setting.&nbsp; In this case I didn't have that option, and needed a quick way to update thousands of files so the EOL chars would match in a binary diff tool.&nbsp; Here's my slightly modified version of <a href="https://stackoverflow.com/a/19132572/2939759" target="_blank">this SO answer</a>:<br /><br /><pre>$items = get-childitem -Path "C:\path\to\dir\" -Recurse -File<br /><br />foreach($original_file in $items)<br />{<br />    $text = [IO.File]::ReadAllText($original_file.FullName) -replace "`r`n", "`n"<br />    [IO.File]::WriteAllText($original_file.FullName, $text)<br />}<br /></pre>
