+++
title = "Auto-Incrementing Build Number in Visual Studio and WiX Installer"
date = 2016-03-20T18:17:00Z
updated = 2016-03-20T18:17:44Z
tags = ["Visual Studio", "WiX", "C-sharp"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

In AssemblyInfo.cs, remove the "AssemblyFileVersion" attribute, and set "AssemblyVersion" to contain "*" where you want to include the revision and build numbers, like 1.5.*<br /><br />In the WiX installer's .wxs file, in the "Product" node, set the "Version" property to look like this:<br /><code>Version="!(bind.FileVersion.FileId)"</code><br />where FileId is the ID of the file to take the version number from.<br /><br />Credit to these two StackOverflow posts:<br /><a href="http://stackoverflow.com/a/826850/2939759">http://stackoverflow.com/a/826850/2939759</a><br /><a href="http://stackoverflow.com/a/641094/2939759">http://stackoverflow.com/a/641094/2939759</a>
