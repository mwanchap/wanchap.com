+++
title = "Testing Sendgrid SMTP without sending emails using sandbox mode"
date = 2019-03-03T17:19:00Z
updated = 2019-03-03T17:19:56Z
tags = ["Sendgrid", "C-sharp"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Here's how to test out a Sendgrid integration using SMTP without actually sending emails.&nbsp; Obviously make sure you have Sendgrid SMTP set up in your config first, and then just add the X-SMTPAPI header (<a href="https://sendgrid.com/docs/for-developers/sending-email/sandbox-mode/" target="_blank">docs link</a>) with some JSON like the below.<br /><br /><br /><pre>MailMessage msg = new MailMessage();<br />var json = @"{<br />    ""mail_settings"": {<br />        ""sandbox_mode"": {<br />            ""enable"": true<br />        }<br />    }<br />}";<br /><br />msg.Headers.Add("X-SMTPAPI", json);<br />// all the usual email stuff<br /><br />SmtpClient smtpclient = new SmtpClient();<br />smtpclient.Send(msg);<br /></pre><div><br /></div>
