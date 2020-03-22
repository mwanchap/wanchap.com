+++
title = "Formats for dealing with dates and datetimes in Salesforce"
date = 2019-04-23T22:09:00Z
updated = 2020-01-05T22:47:18Z
tags = ["Salesforce", "C-sharp"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

The correct way to format dates (not datetimes!) for bulk importing CSVs into Salesforce looks like year-month-day, so today would look like 2019-06-17.&nbsp; These default to the timezone set for the user importing them, so there's no need to convert to UTC.&nbsp; Set this in Excel by<br /><br /><ul><li>Select the column/s containing dates</li><li>Right click on them and select "Format Cells" from the menu</li><li>Select the format "2012-03-14"</li><li>Save as CSV (not the UTF-8 type of CSV)</li></ul><br /><br />For programmatic imports, the correct .NET Framework DateTime format string to use for a Salesforce Date/time is:<br />yyyy-MM-ddTHH:mm:ss.fffZ<br />You can get the same thing in SQL using CONVERT(VARCHAR, datefield, 127) + 'Z'. This also has the added advantage that Excel doesn't interpret it as a date, so you don't have to do the steps above.<br /><br />Regardless of where you're getting the datetime value from, make sure it's in UTC! If the time represents the current moment, use DateTime.UtcNow<br /><br />You might be tempted to use "O" (round-trip pattern) since it looks sort of similar, but don't.&nbsp; It won't cause an error, but the time will be parsed incorrectly.<br /><br />For using timezones instead of UTC (also works for querying Salesforce with SOQL), use a format like:&nbsp;2019-08-01T00:00:00.000+0010<br /><br /><br />
