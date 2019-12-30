+++
title = "Error adding dynamic values to email templates in Dynamics CRM Workflows"
date = 2014-05-01T18:38:00Z
updated = 2014-05-01T18:39:02Z
tags = ["Dynamics CRM 2011"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

This morning I was setting up a new workflow process for sending an email to some users and came across a weird bug. When editing the body of an email, everything was fine until I needed to add a dynamic value from the entity to the email's body, and then as soon as I tried to save, this:<br /><br /><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/-naH86RIrYoo/U2Lyj4v8E4I/AAAAAAAAAHg/Wh4_Ek3w97A/s1600/Capture.JPG" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-naH86RIrYoo/U2Lyj4v8E4I/AAAAAAAAAHg/Wh4_Ek3w97A/s1600/Capture.JPG" height="150" width="320" /></a></div><br />Error details:<br /><blockquote class="tr_bq">Unhandled Exception: System.ServiceModel.FaultException`1[[Microsoft.Xrm.Sdk.OrganizationServiceFault, Microsoft.Xrm.Sdk, Version=5.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35]]: System.Xml.XmlException: Microsoft Dynamics CRM has experienced an error. Reference number for administrators or support: #FD02B69DDetail:<br />&lt;OrganizationServiceFault xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/xrm/2011/Contracts"&gt;<br />&nbsp; &lt;ErrorCode&gt;-2147220970&lt;/ErrorCode&gt;<br />&nbsp; &lt;ErrorDetails xmlns:d2p1="http://schemas.datacontract.org/2004/07/System.Collections.Generic" /&gt;<br />&nbsp; &lt;Message&gt;System.Xml.XmlException: Microsoft Dynamics CRM has experienced an error. Reference number for administrators or support: #FD02B69D&lt;/Message&gt;<br />&nbsp; &lt;Timestamp&gt;2014-05-02T01:15:28.6795291Z&lt;/Timestamp&gt;<br />&nbsp; &lt;InnerFault i:nil="true" /&gt;<br />&nbsp; &lt;TraceText i:nil="true" /&gt;<br />&lt;/OrganizationServiceFault&gt;</blockquote><div>Adding dynamic values to the email subject line or any of the other fields worked fine, it was only in the body where they caused the error. &nbsp;I found the solution <a href="https://community.dynamics.com/crm/f/117/t/125193.aspx">here</a>; turns out it's just a bug in Chrome! &nbsp;I tried again in IE and Firefox and no such problem occurred.</div>