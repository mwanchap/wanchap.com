+++
title = "Visual Studio: Edit and Continue issues"
date = 2018-07-16T17:34:00Z
updated = 2018-07-16T17:34:58Z
tags = ["Visual Studio"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Huge thanks to <a href="https://plus.google.com/118327343052454500232?rel=author" target="_blank">Steve French</a> for this one<br /><br />Like him, I'd been having issues with "Edit and Continue" not working for ages.&nbsp; I tried everything and none of the usual advice helped at all.&nbsp; Finally I came across Steve's post <a href="https://digitaltoolfactory.net/blog/2017/11/fix-problems-edit-continue-visual-studio-2017/" target="_blank">here</a>, and as he suggests, uninstalling Stackify Prefix immediately fixed the problem. Turns out everything was fine to start with, it was just Prefix that was getting in the way (probably due to the way it injects itself into the runtime / server / etc).<br /><br />For reference other settings I tried included:<br />Tools -&gt; Options -&gt; Debugging -&gt; Enable Edit and Continue<br />Project Properties -&gt; Web -&gt; Enable Edit and Continue<br /><br />It kind of sucks because I really liked Prefix, but it's only useful in specific situations, whereas Edit and Continue is much more useful. I guess I'll have to find another profiler...
