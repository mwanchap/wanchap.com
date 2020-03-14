+++
title = "Umbraco's TinyMCE error: 'Cannot read property parentsRequired of undefined'"
date = 2018-01-17T16:07:00Z
updated = 2020-03-13T22:49:21Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

If you find that the "Formats" list in an Umbraco RTE refuses to open, and the Javascript console contains this error:<br /><br /><span style="color: red;">"Cannot read property 'parentsRequired' of undefined"</span><br /><br />Check the stylesheet that the RTE is using.&nbsp; In my case, adding this style had triggered the issue:<br /><br />/**umb_name:Small*/<br />small{}<br /><div><br /></div><div>Although there's nothing wrong with this style itself, the problem is in what TinyMCE considers to be "valid" HTML elements.&nbsp; Why is "small" not valid?&nbsp; No idea!&nbsp; But you can fix this by opening /config/tinyMceConfig.cfg, finding the &lt;validElements&gt; section and appending this:</div><div><br /></div><div>,small[class]</div><div><br /></div><div>And that's it!&nbsp; You can probably substitute "[class]" with other attributes if you need to, or even just [*].&nbsp; I'm not really sure what all the implications of that are (let me know if you find out), so I just went with [class] like some of the other properties have.<br /><br />Credit to&nbsp;Eric Schrepel for helping me figure this one out at&nbsp;<a href="http://issues.umbraco.org/issue/U4-9931">http://issues.umbraco.org/issue/U4-9931</a><br /><br /></div>
