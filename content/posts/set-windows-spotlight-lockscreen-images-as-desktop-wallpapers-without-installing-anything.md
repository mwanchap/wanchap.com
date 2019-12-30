+++
title = "Set Windows spotlight lockscreen images as desktop wallpapers without installing anything"
date = 2019-10-06T18:01:00Z
updated = 2019-10-13T20:41:38Z
tags = ["Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I ended up moving the code for this post into my github since I'm using it myself ;) Get it from here:
<a href="https://github.com/mwanchap/configs/blob/master/Scripts/Windows%20Spotlight%20Wallpapers.ps1"> https://github.com/mwanchap/configs/blob/master/Scripts/Windows%20Spotlight%20Wallpapers.ps1 </a><br /><br />Once you've cloned it, the only things you need to do are:<br /><br /><ul><li>Decide where you want the wallpaper images to go</li><li>Update the $location variable in the script with that location (I'm using ~\Pictures\Spotlight Wallpapers)</li><li>Run the script</li><li>Open windows background settings and set the background type to "slideshow", pointed at that location</li><li>Run the script at startup if you want to get new images all the time (optional but recommended)</li></ul><br /><br /><br />

