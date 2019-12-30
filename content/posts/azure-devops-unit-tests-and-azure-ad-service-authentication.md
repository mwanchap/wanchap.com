+++
title = "Azure Devops, unit tests and Azure AD Service Authentication"
date = 2018-11-26T21:28:00Z
updated = 2018-11-27T20:20:15Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I couldn't think of a title for this one that wasn't ridiculously long so to help future Googlers, here's what we were trying to do:<br /><br /><ul><li>Authenticate against Azure Key Vault</li><li>using a Service Principal</li><li>using Azure AD Service Authentication</li><li>Rrom our build server</li><li>Running an Azure Devops build agent</li></ul><br />Whew.&nbsp; Basically we had some integration tests that retrieve a database connection string from an Azure Key Vault, and needed Azure Devops to be able to run those tests on our build server. Which meant it has to authenticate with its own service principal in Azure AD as described in here:&nbsp;<a href="https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#running-the-application-using-a-service-principal">https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#running-the-application-using-a-service-principal</a><br /><br />We were using the certificate-based method, to request a token to access the Key Vault, but it wasn't working :(&nbsp; In case I run into this again, here's the steps we had to go through to sort it out:<br /><br /><br /><ol><li>Don't get the cert thumbprint from the certificate properties, get them from Powershell where it'll be formatted properly without all the spaces</li><li>Remove all the braces from the environment variable.&nbsp; It sounds obvious in retrospect but considering how often things that have to be {formatted_like_this}, we missed it.</li><li>Add the Service Principal's <i>Application</i>&nbsp;(not the service principal itself) to the Key Vault</li><li>Change the build agent to run as "Local System" account - it installs itself as "Network Service" by default, but that account didn't have access to the cert store that we had put the certificate in.&nbsp; There's probably a better way to do this - let me know what it is!</li></ol>
