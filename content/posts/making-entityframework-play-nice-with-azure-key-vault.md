+++
title = "Making EntityFramework play nice with Azure Key Vault"
date = 2018-11-14T18:15:00Z
updated = 2018-11-19T15:34:51Z
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Make a separate class containing a constructor to pass in the connection string from KV.&nbsp; Don't modify the constructor in the Whatever.Context.cs file because it'll get regenerated when you update the model and overwrite any changes you make in there.<br /><br />Get the connection string from the "update model from database" command, but replace &amp;quot; with actual quotes. The connection string in KV should look like this:<br /><br />metadata=res://*/EntityFramework.DataWarehouse.csdl|res://*/EntityFramework.DataWarehouse.ssdl|res://*/EntityFramework.DataWarehouse.msl;provider=System.Data.SqlClient;provider connection string="data source=databasename.database.windows.net;initial catalog=thedatabase;user id=dbusername;password=passwordgoeshere;MultipleActiveResultSets=True;App=EntityFramework"
