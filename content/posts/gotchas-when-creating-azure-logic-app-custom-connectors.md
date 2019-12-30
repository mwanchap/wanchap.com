+++
title = "Gotchas when creating Azure Logic App Custom Connectors"
date = 2019-01-22T17:20:00Z
updated = 2019-01-22T17:20:32Z
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

We created a custom connector for a SOAP service and had to import the WSDL<br /><br />If the WSDL contains any wsdl:import elements, the import will fail since the UI doesn't know how to deal with them.&nbsp; You'll have to "flatten" the WSDL, which follows each import element to the linked WSDL, then follows imports in those files and so on until it can sticks them all together.&nbsp; There's a tool that does this <a href="https://shulerent.com/2013/03/14/generating-a-single-flattened-wsdl-from-an-existing-wcf-service/#comment-2208" target="_blank">here</a>.<br /><br />Don't remove any of the generated actions!&nbsp; The UI will throw errors at you if the Swagger it generates from the WSDL you imported doesn't match up with all the actions.
