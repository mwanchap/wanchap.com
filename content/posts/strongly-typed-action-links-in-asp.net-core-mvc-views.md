+++
title = "Strongly-typed action links in ASP.NET Core MVC views"
date = 2018-09-30T23:16:00Z
updated = 2018-09-30T23:16:16Z
tags = ["Visual Studio", "ASP.NET", "Nuget", ".NET Core"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

While experimenting with ASP.NET Core and Razor views it occurred to me that the magic-string-based links really weren't ideal, so I did a little googling and came across the excellent <a href="https://github.com/ivaylokenov/AspNet.Mvc.TypedRouting" target="_blank">AspNet.Mvc.TypedRouting</a> nuget package, which lets you use strongly-typed references to controllers and action methods.<br /><br />I won't repeat the install instructions, but for some reason they didn't provide any examples of using their extension methods with the one thing I wanted to do - action links.&nbsp; For future reference, here's an example of how to use them in a Razor view<br /><br /><code>&lt;li&gt;@( Html.ActionLink&lt;AppController&gt;("Home", c =&gt; c.Index()) )&lt;/li&gt;<br />&lt;li&gt;@( Html.ActionLink&lt;AppController&gt;("Test", c =&gt; c.Test()) )&lt;/li&gt;<br /><br /></code><br /><div><br /></div>
