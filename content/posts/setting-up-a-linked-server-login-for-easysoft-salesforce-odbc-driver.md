+++
title = "Setting up a Linked Server login for EasySoft Salesforce ODBC Driver"
date = 2016-01-20T17:08:00Z
updated = 2016-01-20T17:08:09Z
tags = ["Salesforce", "T-SQL", "Dynamics CRM 2011"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

We're currently using EasySoft's excellent <a href="http://www.easysoft.com/products/data_access/odbc-salesforce-driver/">Salesforce ODBC Driver</a> to be able to treat our Salesforce org as if it were another SQL database (really useful for updating legacy stored procedures by rewriting queries that reference migrated Dynamics tables to query Salesforce instead!)  We were working on updating a particular page in our website that needed to use it but was running into permissions issues when querying it, the error was:<br /><br /><code><span style="color: red;">Access to the remote server is denied because no login-mapping exists</span></code><br /><br />For future reference, this means that the account the website was connecting with wasn't granted permission to connect to the ODBC driver since it's set up as a "Linked Server", and SQL server doesn't just let you query those unless you've got sysadmin privileges, or unless the account is specifically set up to connect to them.  Here's the code I used to resolve the issue:<br /><br /><pre>--removing previous login, because I had to tweak this a few times<br />exec sp_droplinkedsrvlogin @rmtsrvname= 'easysoft connection name' , <br />     @locallogin= 'db login name'<br /><br />exec sp_addlinkedsrvlogin @rmtsrvname = 'easysoft connection name',<br />     @locallogin =  'db login name',<br />     @useself = false,   --defaults to true and ignores the below<br />     @rmtuser = 'salesforce username', --already specified in easysoft config, still have to specify it here for some reason<br />     @rmtpassword = 'salesforce pw'<br /></pre>
