+++
title = "Authentication error querying Dynamics CRM OrganisationService"
date = 2015-05-02T21:28:00Z
updated = 2015-05-22T18:59:38Z
tags = ["C#", "Dynamics CRM 2011", "IIS"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

An IIS website we had that queries the Dynamics CRM (2011) OrganisationService was getting<br /><pre>"[SecurityNegotiationException: The caller was not authenticated by the service.]"</pre><br />Thrown back at it when being accessed under certain circumstances (I forget exactly what they were, although I do remember it being a huge pain in the butt). The Service was instantiated using <code>CredentialCache.DefaultNetworkCredentials</code> as in many examples. The problem was that those client credentials were not being impersonated correctly even though impersonation and windows auth was enabled in IIS.<br /><br />Turns out the solution was to add an <pre>[OperationBehavior(Impersonation = ImpersonationOption.Required)]</pre> attribute to any methods that tried to query the OrganisationService!
