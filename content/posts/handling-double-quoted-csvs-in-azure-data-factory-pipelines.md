+++
title = "Handling double-quoted CSVs in Azure Data Factory Pipelines"
date = 2019-06-12T19:39:00Z
updated = 2019-06-13T20:44:13Z
tags = ["Azure Data Factory", "Azure"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Azure Data Factory by default uses a backslash as the escape character for CSVs, but we ran into an issue with this today processing one of the CSV files from data.gov.au.&nbsp; As with most CSVs they use quotes around values as normal and with double-quotes for empty values, but they also use double-quotes to <i>escape </i>quotes within non-empty values. This probably sounds confusing, so here's an example:<br /><br />"column 1","column 2",<span style="background-color: yellow;">""</span>,"column 4 value is <span style="background-color: yellow;">""</span>sort of<span style="background-color: yellow;">""</span> like this"<br /><br />The ADF pipeline failed because the double-quotes don't get escaped correctly:<br />ErrorCode=UserErrorSourceDataContainsMoreColumnsThanDefined, found more columns than expected column count.<br /><br />The solution was to change the "Escape character" property on the dataset, by clicking the "Edit" button beneath it and manually entering "", since "" isn't in the list of escape characters.&nbsp; I didn't think this would work at first but it turns out that escape characters don't have to be a single character, and it looks like the double-quotes used for empty values are processed separately from double-quotes used as escape characters.&nbsp; Handy!<br /><br />Edit:<br />Unfortunately you can't just set "" as an escape character when creating the dataset, because even though it can process the CSV correctly when set this way, ADF will give you an error when importing the schema for the CSV:<br /><br />"CSV serilization setting escapeChar cannot be more than one character"<br /><br />So the trick is to leave it as backslash, just to import the schema, and then change it to double-quotes afterwards, since this seems to be the only step that complains about this escape character.
