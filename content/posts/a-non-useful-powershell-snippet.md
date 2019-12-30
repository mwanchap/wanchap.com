+++
title = "A non-useful Powershell snippet"
date = 2018-10-02T16:55:00Z
updated = 2018-10-02T16:55:43Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

What can I say, I was distracted<br /><br />$t = "Taste the rainbow "; $c = ([ConsoleColor].GetEnumNames()); (1..7) | % {$c += $c; $t += $t}; foreach($x in $c) { write-host $t -ForegroundColor $x -NoNewline; sleep -Milliseconds 50 }
