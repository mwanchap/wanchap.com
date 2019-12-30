+++
title = "Get current user in Dynamics CRM SSRS report"
date = 2014-05-26T14:58:00Z
updated = 2014-05-26T14:58:24Z
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

<br />select fullname<br />from FilteredSystemUser<br />where systemuserid = dbo.fn_FindUserGuid()<br /><br />Don't use&nbsp;User!UserID<br /><br />Refer to&nbsp;http://crmtipoftheday.com/2014/01/09/reflecting-current-user-ssrs/<br /><br />
