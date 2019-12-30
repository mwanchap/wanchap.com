+++
title = "Stopping Dynamics CRM from auto-creating contacts from tracked Outlook emails"
date = 2013-11-11T17:05:00Z
updated = 2013-11-11T17:05:49Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I encountered an issue today where any time one of several users attempted to track an email in Dynamics CRM (2011) from within their Outlook client it would create contact records in CRM for whoever the email was sent to. &nbsp;I knew this was a setting in CRM somewhere and found it in the settings dialog here:<br /><br /><div class="separator" style="clear: both; text-align: center;"><a href="http://4.bp.blogspot.com/-lHcFLYWen54/UoF9-ifJ6hI/AAAAAAAAAE8/aP5nTkQ1E5I/s1600/crmemail.JPG" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="255" src="http://4.bp.blogspot.com/-lHcFLYWen54/UoF9-ifJ6hI/AAAAAAAAAE8/aP5nTkQ1E5I/s320/crmemail.JPG" width="320" /></a></div><br />However I didn't want to go through all the annoyance of instructing everyone affected to manually alter the setting, so I fixed the problem once-and-for-all (at least until we get more users) by updating it for everyone in the CRM database. &nbsp;The relevant field is AutoCreateContactOnPromote&nbsp;in dbo.UserSettingsBase. &nbsp;Just set it to 0 and you're done!
