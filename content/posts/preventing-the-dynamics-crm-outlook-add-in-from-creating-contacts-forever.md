+++
title = "Preventing the Dynamics CRM Outlook add-in from creating contacts, forever"
date = 2014-09-25T23:07:00Z
updated = 2014-09-25T23:07:24Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

It's an ongoing issue here wherein a&nbsp;misconfigured / misbehaving Outlook client sometimes creates duplicate or redundant contacts in our CRM, and I've seen many blog posts and forum threads discussing the various ways of getting around it. &nbsp;Unfortunately they all require user-specific configuration, whereas I wanted to banish the problem across the board once-and-for-all. &nbsp;Completely by accident I came across a solution, which in retrospect is extremely obvious and I'm rather embarrassed that I didn't figure it out sooner!<br /><br />It all hinges on the fact that the Dynamics CRM website will execute javascript on the form, and of course the Outlook add-in will not, as no form is loaded (although there is a way to get one, which is covered here too).<br /><br />Add a boolean field to your contact entity called "Permit Creation", which defaults to no.<br />Add it to the contact form, but mark it as hidden.<br />Add the following javascript to the contact form in the page load event:<br /><br />if(!Xrm.Page.context.isOutlookClient() &amp;&amp; Xrm.Page.ui.getFormType() == 1)<br />{<br /><span class="Apple-tab-span" style="white-space: pre;"> </span>Xrm.Page.getAttribute["new_permitcreation"].setValue(true);<br />}<br /><br /><i>(The isOutlookClient() / getFormType() check isn't really needed for this, but prevents people from accidentally creating contacts via forms in Outlook too, if that's what you want)</i><br /><br />Next, create a CRM plugin using Visual Studio that does the following:<br />(obviously this is not the complete plugin code, just the part that matters)<br /><br />bool permitted = (bool)entity.Attributes["new_permitcreation"];<br />if(!permitted)<br />{<br />&nbsp; &nbsp; &nbsp; &nbsp; throw new InvalidPluginExecutionException("Contacts may only be created via the CRM website.");<br />}<br /><br />Easy!
