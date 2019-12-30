+++
title = "Dynamics CRM - Globally Disable Outlook Plugin Auto Create Contact"
date = 2014-07-13T22:29:00Z
updated = 2014-07-13T22:29:20Z
tags = ["T-SQL", "Dynamics CRM 2011"]
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

We've had a recurring problem here where new users ...<br />auto-create contacts from outlook<br />put a picture of it<br /><br />Finally found a tool that does this from:<br />http://mscrmshop.blogspot.com.au/2013/04/how-to-disable-convert-incoming-email.html<br /><br />I was curious as to how it worked so I poked around in ILSpy and found the following:<br /><br />The actual setting involved is:<br /><br />SELECT &nbsp;orgdborgsettings<br />FROM &nbsp; &nbsp;FilteredOrganization<br /><br />And the actual value that is set for this particular attribute is:<br /><br />"&lt;OrgSettings&gt;&lt;AutoCreateContactOnPromote&gt;True&lt;/AutoCreateContactOnPromote&gt;&lt;/OrgSettings&gt;"<br /><br />So if you're comfortable with XML you could actually just apply the values in that field directly, but I'd advise against that since CRM would probably flip its wig if you got one character wrong.
