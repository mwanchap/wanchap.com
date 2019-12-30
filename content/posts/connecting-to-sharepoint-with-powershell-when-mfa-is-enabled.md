+++
title = "Connecting to Sharepoint with Powershell when MFA is enabled"
date = 2019-10-20T19:29:00Z
updated = 2019-10-20T19:56:01Z
tags = ["Azure", "Powershell", "Sharepoint Online"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

If you're using multifactor auth, the usual login method mentioned in the SPOService documentation isn't going to work (using Get-Credential) and you'll get an error saying "Connect-SPOService : The sign-in name or password does not match one in the Microsoft account system".<br /><br />The correct process is rather bizarre:<br /><br />$orgName = "organizationname"<br />connect-sposervice -url "https://$orgName-admin.sharepoint.com"<br /><br />Then you'll get the same Azure AD auth popup that you'd get with Connect-AzureRmAccount and Microsoft's other Powershell modules.&nbsp; The only place I could find this was in Microsoft's docs <a href="https://docs.microsoft.com/en-us/powershell/sharepoint/sharepoint-online/connect-sharepoint-online?view=sharepoint-ps#to-connect-with-multifactor-authentication-mfa" target="_blank">here</a>, but it would have saved me some time if it was at least mentioned in the help text for Connect-SPOService...
