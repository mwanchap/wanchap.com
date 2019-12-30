+++
title = "Resolving ASP.NET MVC DLL hell"
date = 2018-10-29T01:50:00Z
updated = 2018-10-29T01:50:11Z
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Reinstall all nuget packages with package manager console:<br />Update-Package -Reinstall<br /><br />For the System.Net.Http one:<br />&lt;dependentAssembly&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &lt;assemblyIdentity name="System.Net.Http" publicKeyToken="b03f5f7f11d50a3a" culture="neutral"/&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &lt;bindingRedirect oldVersion="0.0.0.0-4.2.0.0" newVersion="4.0.0.0"/&gt;<br />&nbsp; &nbsp; &nbsp; &lt;/dependentAssembly&gt;<br /><br />For the&nbsp;Microsoft.Rest.ClientRuntime one, install the nuget package<br /><br />For the system.runtime one:<br />&lt;dependentAssembly&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &lt;assemblyIdentity name="System.Runtime" publicKeyToken="b03f5f7f11d50a3a" culture="neutral"/&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &lt;bindingRedirect oldVersion="0.0.0.0-4.1.2.0" newVersion="4.0.0.0"/&gt;<br />&nbsp; &nbsp; &nbsp; &lt;/dependentAssembly&gt;<br /><br />Attempt 2:<br />Reset all projects to use .NET framework 4.7.1<br />Uninstall / reinstall the nuget pkgs below<br /><br />Attempt 3 - works locally, works in Azure<br />Uninstall/reinstall the following nuget packages from all projects<br />get-project -All | uninstall-package&nbsp;Microsoft.Extensions.Configuration.AzureKeyVault<br />get-project -All | uninstall-package Microsoft.Azure.KeyVault<br />get-project -All | uninstall-package Microsoft.Azure.KeyVault.WebKey<br />get-project -All | uninstall-package SimpleInjector.Integration.WebApi<br />get-project -All | uninstall-package SimpleInjector.Integration.Web.Mvc<br />get-project -All | uninstall-package SimpleInjector.Integration.Web<br />get-project -All | uninstall-package SimpleInjector<br />Add the binding redirect for system.net.http above
