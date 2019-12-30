+++
title = "IIS secured local debugging"
date = 2018-08-23T21:28:00Z
updated = 2018-08-29T15:39:08Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Download and run this:<br /><a href="https://github.com/mwanchap/configs/blob/master/SetupLocalhostCerts.ps1">https://github.com/mwanchap/configs/blob/master/SetupLocalhostCerts.ps1</a><br /><br />For each project:<br /><br /><ul><li>Open Visual Studio</li><li>In Solution Explorer, select the web project and press F4 to open properties (not right click -&gt; Properties, that's a different set of properties for some reason)</li><li>Set "SSL Enabled" = True</li><li>Copy the SSL URL</li><li>Right click on the project name in Solution Explorer again and open Properties from there</li><li>Select "Web" section</li><li>Paste SSL URL into "Project Url"</li></ul><div>TODO: script to enable edit-and-continue for local IIS</div><div><br /></div><div>Credit:</div><div>PS script derived from a similar one by&nbsp;camieleggermont at <a href="https://gist.github.com/camieleggermont/5b2971a96e80a658863106b21c479988">https://gist.github.com/camieleggermont/5b2971a96e80a658863106b21c479988</a></div><div>Enabling Edit-and-Continue for Local IIS from&nbsp;<a href="https://stackoverflow.com/a/50509545/2939759">https://stackoverflow.com/a/50509545/2939759</a></div><div><br /></div>
