+++
title = "OTF fonts (e.g. Fira Code) look nasty on gVim in Windows"
date = 2019-11-10T15:23:00Z
updated = 2019-11-11T15:02:24Z
tags = ["Vim"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I really like the "Fira Code" font but it always looked <i>nasty</i>&nbsp;in gVim on Windows (my main text editor besides VS), and I really don't want to use a different font for each editor. After spending literally hours fiddling with stuff like the guifont setting, different font/size combos, custom font renderers (e.g. MacType), I finally realised the fonts themselves aren't the problem, nor the rendering settings.&nbsp; The problem was that the chocolatey installer I had used installed OTF versions of the files, which gVim always used by default even if the TTF versions of them were installed. Uninstalling OTFs and installing TTFs fixed the problem immediately, and now once again I have consistent font rendering across all my text editors. Hooray.<br /><br />Bonus font opinions:<br />Best: Fira Code, Cascadia Code, Source Code Pro (in that order)<br />Nope: Envy Code R, Inconsolata, Hack, Oxygen Mono, Anonymous Pro
