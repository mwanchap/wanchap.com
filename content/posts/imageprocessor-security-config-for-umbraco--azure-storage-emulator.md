+++
title = "ImageProcessor security config for Umbraco + Azure Storage Emulator"
date = 2019-09-29T22:58:00Z
updated = 2019-09-29T23:04:07Z
tags = ["Umbraco", "Azure"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

This is only going to work if you're using ImageProcessor with Umbraco to deal with images being loaded from blob storage in the Azure Storage Emulator. Took me a while to get the settings right, the way I figured it out was:<br /><br /><ul><li>firstly, use Azure Storage Explorer to find the URL for your emulated blob container and make sure that works by requesting from there directly</li><li>Find the URL it's attempting to use by catching the ImageProcessingExceptions that get thrown when it can't find the file</li></ul><br />Once I had both the correct URL as well as the URL that it was attempting to use, figuring out what to put in the config was just trial and error.&nbsp; Here's what I ended up with:<br /><br /><pre>&lt;service name="CloudImageService" <span style="background-color: yellow;">prefix="media"</span> type="ImageProcessor.Web.Services.CloudImageService, ImageProcessor.Web"&gt;<br />    &lt;settings&gt;<br />        &lt;setting key="Container" value="<span style="background-color: yellow;">devstoreaccount1/media</span>"/&gt;<br />        &lt;setting key="MaxBytes" value="16777216"/&gt;<br />        &lt;setting key="Timeout" value="30000"/&gt;<br />        &lt;setting key="Host" value="<span style="background-color: yellow;">http://127.0.0.1:10000</span>"/&gt;<br />    &lt;/settings&gt;<br />&lt;/service&gt;<br /></pre><br />The tricky part was that the instructions on the ImageProcessor website say to put the container name inside the "Host" value, which didn't seem to work. They also don't mention that the "container" value there isn't actually the name of the "blob container" itself but the full path to where Umbraco's media filesystem lives. Also, that "prefix" value was confusing, it seems to be more about which URL to catch requests for, rather than anything to do with the blob storage or file path etc.
