+++
title = "Get the date each branch in a git repo diverged from master"
date = 2018-12-12T23:26:00Z
updated = 2018-12-13T16:21:56Z
tags = ["bash", "git"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I'm trying to clean up some long-lived branches in our repo and came across <a href="https://stackoverflow.com/a/28110167/2939759" target="_blank">this handy stackoverflow post</a> to get branches by the date of the commit they branched from.<br /><br />I've modified it slightly to be easier to use for my purposes:<br />git show-ref | { while read branch; do merge_base=$(git merge-base --all $branch master); date_branched=$(git show -s --format=format:"%cd %an" --date=short $merge_base); echo "$date_branched, $branch"; done } | sort
