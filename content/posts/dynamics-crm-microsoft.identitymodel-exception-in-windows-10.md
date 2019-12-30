+++
title = "Dynamics CRM Microsoft.IdentityModel exception in Windows 10"
date = 2018-06-04T18:58:00Z
updated = 2018-06-04T21:28:44Z
tags = ["Dynamics CRM 2011"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

When trying to connect to Dynamics CRM services on a Windows 10, machine, you might get this error:<br /><br />Could not load file or assembly ‘Microsoft.IdentityModel, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35’ or one of its dependencies<br /><br />There are plenty of blog posts around that will all tell you to go and install "Windows Identity Foundation", however this is no longer the case for Windows 10 and the installer for WIF will fail.&nbsp; This is because it's now a Windows feature - install it via the "Turn Windows features on or off" section in "Programs and Features" as mentioned <a href="https://dynamicsofdynamicscrm.com/2015/09/11/quick-tipenabling-windows-identity-foundation-on-windows-10-machines/" target="_blank">here</a>.
