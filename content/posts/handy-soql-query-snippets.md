+++
title = "Handy SOQL query snippets"
date = 2019-06-04T15:13:00Z
updated = 2019-06-04T15:13:18Z
tags = ["Salesforce"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

To count how many people logged in for the last time each year, for only inactive users:<br /><br /><span style="font-family: Courier New, Courier, monospace;"><span style="background-color: white; border: 0px; font-size: 16px; font-stretch: inherit; font-variant-east-asian: inherit; font-variant-numeric: inherit; line-height: inherit; margin: 0px; padding: 0px; vertical-align: baseline;">select calendar_year(lastlogindate) LoginYear,</span><span style="background-color: white; font-size: 16px;">count(id) Total</span><br style="background-color: white; font-size: 16px;" /><span style="background-color: white; font-size: 16px;">from user</span><br style="background-color: white; font-size: 16px;" /><span style="background-color: white; font-size: 16px;">where isactive = false</span><br style="background-color: white; font-size: 16px;" /><span style="background-color: white; font-size: 16px;">and lastlogindate &lt;&gt; null</span><br style="background-color: white; font-size: 16px;" /><span style="background-color: white; font-size: 16px;">group by calendar_year(lastlogindate)</span><br style="background-color: white; font-size: 16px;" /><span style="background-color: white; font-size: 16px;">order by count(id) desc</span></span><br /><span style="background-color: white; font-family: Calibri, Arial, Helvetica, sans-serif; font-size: 16px;"><br /></span><span style="background-color: white; font-family: Calibri, Arial, Helvetica, sans-serif; font-size: 16px;"><br /></span>
