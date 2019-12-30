+++
title = "Scribe Agent Issues"
date = 2015-12-02T18:21:00Z
updated = 2015-12-02T18:21:56Z
tags = ["Salesforce", "Scribe Online", "Dynamics CRM 2011"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Today we encountered a weird problem after resetting the credentials for the Salesforce account used for synchronising data.  Although the "Test Connection" was successful, any attempts to connect to Salesforce ended up with this error:  "Destination URL not reset. The URL returned from login must be set in the SforceService SOQL"  Which really doesn't help much; Googling for it just turns up a bunch of info about Salesforce API connections, so hopefully someone having the same issue finds this post.  Eventually we solved the issue by unchecking the "API-only user" setting in the profile, resetting the account's security token (even though none is ever needed elsewhere, as it's an IP-restricted profile) and then restarting the Scribe Agent on our server.  Scribe's ambiguous error reporting continues to be pretty unhelpful...
