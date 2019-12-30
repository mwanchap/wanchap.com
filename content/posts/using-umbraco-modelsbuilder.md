+++
title = "Using Umbraco ModelsBuilder"
date = 2017-11-27T17:31:00Z
updated = 2017-12-13T22:58:17Z
tags = ["Umbraco"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Firstly, make sure the following properties are set in your solution's top-level web.config to enable the models builder:<br /><br />&lt;add key="Umbraco.ModelsBuilder.Enable" value="true"/&gt;<br />&lt;add key="Umbraco.ModelsBuilder.ModelsMode" value="LiveAppData"/&gt;<br /><div><br /></div><div>I like the "LiveAppData" mode, but you should experiment with the others from the list in the ModelsBuilder docs&nbsp;<a href="https://github.com/zpqrtbnk/Zbu.ModelsBuilder/wiki/Builder-Modes" target="_blank">here</a>.&nbsp; Generate your model classes, and include them in the VS Solution.</div><div><br /></div>Unless you're on a brand new project, any existing views will need to be modified.<br /><br /><h4>Model class inheritance</h4>Change instances of<br />@inherits Umbraco.Web.Mvc.UmbracoTemplatePage<br />to<br />@inherits Umbraco.Web.Mvc.UmbracoViewPage&lt;ContentModels.ModelName&gt;<br /><br /><h4>Property Access</h4><div>Change instances of</div><div>@Umbraco.Field("propertyAlias")</div><div>to</div><div>@Model.PropertyAlias</div><div>Note that the ModelsBuilder converts property aliases to PascalCase instead of camelCase</div><div><br /></div><h4>Rendering Grid HTML</h4>Change instances of<br />@CurrentPage.GetGridHtml("gridProperty")<br />to<br />@Html.GetGridHtml(Model, "gridProperty")<br /><br /><h4>Getting URLs for Image Properties</h4><div>No more passing around image IDs or calling Umbraco.TypedMedia!&nbsp; Make sure you can use C# 6 language features (Install-Package Microsoft.Net.Compilers) and just do this:</div><div>String imageUrl = Model.ImageProperty?.Url;</div>
