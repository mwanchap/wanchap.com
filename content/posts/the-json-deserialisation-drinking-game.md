+++
title = "The JSON deserialisation drinking game"
date = 2014-05-27T18:50:00Z
updated = 2014-05-27T18:50:24Z
tags = ["JSON", "jQuery"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Take a drink every time you see this pattern:<br /><br /><code>$.ajax({<br />&nbsp; &nbsp; data: "{things:stuff}",<br />&nbsp; &nbsp; dataType: "json",</code><br /><code>&nbsp; &nbsp; //other properties omitted<br />&nbsp; &nbsp; success: function (result) {<br />&nbsp; &nbsp; &nbsp; &nbsp; var myObject =&nbsp;<span style="background-color: yellow;">eval</span>( "(" +&nbsp;result.d + ")"&nbsp;); //noooooooooooooooo<br />&nbsp; &nbsp; }<br />});</code><br /><br />Take a drink when someone seriously brings up the catchphrase "eval is evil" or a variant of it.<br /><br />Finish all of the drinks if you sincerely think that nobody would ever get malicious code into your database/application that will be happily executed when eval evaluates it and send your client to their phishing duplicate of your login page where they harvest user credentials before redirecting them right back to your application so nobody ever realises what just happened.<br /><br />Aside:<br />"Eval is not evil" in the same way that dynamic SQL is not evil. But in this case it's bad, and wrong. &nbsp; JSON.parse is how to parse JSON.<br /><br />
