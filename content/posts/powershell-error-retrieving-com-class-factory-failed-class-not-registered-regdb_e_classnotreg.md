+++
title = "Powershell error: Retrieving COM class factory failed: class not registered (REGDB_E_CLASSNOTREG)"
date = 2019-11-05T17:55:00Z
updated = 2019-11-05T17:55:00Z
tags = ["Powershell", "IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

The problematic command and full error message was:<br /><br />&gt;get-webbinding<br /><span style="color: red;">"get-webconfigurationproperty : Retrieving the COM class factory for component with CLSID {688EEEE5-6A7E-422F-B2E1-6AF00DC944A6} failed due to the following error: 80040154 Class not registered (Exception from HRESULT: 0x80040154 (REGDB_E_CLASSNOTREG))."</span><br /><br />I was pretty stuck on the above error while trying to run a script for setting up sites in IIS which involved some calls to get-webbinding (in the WebAdministration module). After much digging around I finally ran into <a href="https://forums.iis.net/post/1997521.aspx" target="_blank">this post</a>. Turns out, genius that I am, I&nbsp;had created a shortcut to the x86 version of Powershell when I first created the VM, so I'd been using the wrong bitness&nbsp;<i>the entire time</i>. I'm surprised I didn't have more issues!&nbsp; Anyway, running the 64-bit (i.e. regular)&nbsp;version of Powershell fixed the problem immediately. Thanks jasonint32 ;)<br /><br /><br />
