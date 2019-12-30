+++
title = "Azure AD error - IDX10311: RequireNonce is true but validationContext.Nonce is null"
date = 2019-03-27T19:28:00Z
updated = 2019-03-27T19:28:10Z
tags = ["Active Directory", "Azure", "C#"]
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I've experienced this one enough times now that I'd like to preserve the solution/s for future occurrences. The exact message is:<br /><blockquote class="tr_bq">IDX10311: RequireNonce is 'true' (default) but validationContext.Nonce is null. A nonce cannot be validated. If you don't need to check the nonce, set OpenIdConnectProtocolValidator.RequireNonce to 'false'.</blockquote><div>An easy way to reproduce this one is to hit the "back" button after having signed in to an ASP.NET web app that auths with Azure AD using the OWIN library.<br /><br /><a href="https://stackoverflow.com/questions/29502788/enabling-ssl-in-asp-net-mvc-5-app-results-in-openidconnectprotocolvalidator-issu">https://stackoverflow.com/questions/29502788/enabling-ssl-in-asp-net-mvc-5-app-results-in-openidconnectprotocolvalidator-issu</a></div>
