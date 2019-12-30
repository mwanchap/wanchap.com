+++
title = "Installing SQL Server Express to set up an Azure database locally"
date = 2018-06-27T16:43:00Z
updated = 2018-06-27T16:43:57Z
tags = ["Azure", "SQL Server"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

<br /><h4>Installing SQL Express:</h4><ol><li>Download SQL Express installer</li><li>Switch to an account with full local admin permissions (our regular accounts don't have these so I had to use a global admin account instead) and install SQL Express with that account</li><li>Once installation completes, make a note of the connection string you're given on the final page of the installer</li><li>Open SSMS and connect to the database - default name is localhost\sqlexpress</li><li>Navigate to Security -&gt; Logins -&gt; New Login</li><li>Add the regular (non-admin) domain account that you'll be using most of the time</li><li>Once added, open that account under the Logins section and then open the "Server Roles" page</li><li>Add the account to the "sysadmin" role</li></ol><h4>Obtaining the Azure database:</h4><div><ol><li>Open the database and select the "Export" option at the top of the "Overview" page</li><li>Choose a storage account and container to drop the export file in and enter the server admin creds</li><li>Once the file has been created, access that storage container and download the db export file</li></ol></div><h4>Restoring the export file</h4><div><ol><li>Back in SSMS, connect to your local SQL express server instance again (if it isn't still connected), right-click on the "Databases" node and select "Import Data-tier Application"</li><li>Select the db export file, give the database a name, click "Next"</li></ol><div>Don't forget to update connection strings in your applications ;)&nbsp; If they're running under your normal account (i.e. not a separate app pool account etc), it should look something like "Server=localhost\sqlexpress;Database=[your database name];Trusted_Connection=True;"</div></div><div><br /></div><div>(This is obviously for local development and testing only; if you set up a real server like this, you're insane)</div>
