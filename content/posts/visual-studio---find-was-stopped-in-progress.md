+++
title = "Visual Studio - 'Find was stopped in progress'"
date = 2014-05-29T16:08:00Z
updated = 2020-03-13T22:49:47Z
tags = ["Visual Studio"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Sometimes you'll do a Find for "Entire Solution" (Ctrl&nbsp;+ Shift&nbsp;+ F is a handy shortcut) and instead of finding anything, the "Find Results" window will immediately display "Find was stopped in progress" with zero results. &nbsp;I usually deal with it by restarting Visual Studio or my computer, but this time I decided to actually look into it. &nbsp;Turns out it was a lot more common than I thought and is apparently a Windows bug, not Visual Studio, and goes way back to 2004.<br /><br />Anyway, the solution is to click in the "Find Results" dialog so the cursor appears and mash Break, Ctrl+Break,&nbsp;Alt+Break and Ctrl+ScrLock&nbsp;key combos, perhaps while a find is in progress (although mine wasn't and it still worked, but ymmv).<br /><br />There's also this extension which claims to help:&nbsp;<a href="http://visualstudiogallery.msdn.microsoft.com/23d270a7-c74c-47e4-ba14-d9341e9017ff">http://visualstudiogallery.msdn.microsoft.com/23d270a7-c74c-47e4-ba14-d9341e9017ff</a><br /><br />Source:&nbsp;<a href="http://stackoverflow.com/questions/259398/visual-studio-find-results-in-no-files-were-found-to-look-in-find-stopped-pr">http://stackoverflow.com/questions/259398/visual-studio-find-results-in-no-files-were-found-to-look-in-find-stopped-pr</a>
