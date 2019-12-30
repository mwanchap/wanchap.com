+++
title = "Adding Application Insights to a .NET Core application"
date = 2018-09-20T13:37:00Z
updated = 2018-09-30T23:17:14Z
tags = ["MVC", "Visual Studio", "ASP.NET", "Azure", "C#", ".NET Core"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

$appInsights = New-AzureRmApplicationInsights -Location USEast -ResourceGroupName rgname -Name ainame<br />$appInsights.InstrumentationKey #copy this<br /><br />dotnet new mvc<br />dotnet add package Microsoft.ApplicationInsights.AspNetCore<br /><br />In appsettings.json, add this<br />{<br />&nbsp; "ApplicationInsights": {<br />&nbsp; &nbsp; "InstrumentationKey": "11111111-2222-3333-4444-555555555555"<br />&nbsp; }<br />}<br /><br />In program.cs add UseApplicationInsights() to the method chain for CreateDefaultBuilder<br /><br />dotnet run<br /><br />Ref:&nbsp;https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started-with-Application-Insights-for-ASP.NET-Core<br /><br />
