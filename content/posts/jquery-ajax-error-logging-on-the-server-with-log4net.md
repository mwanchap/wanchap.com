+++
title = "jQuery ajax error logging on the server with log4net"
date = 2014-09-17T22:23:00Z
updated = 2014-09-17T22:23:02Z
tags = ["ASP.NET", "log4net", "Javascript", "jQuery"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

This post is based on <a href="http://www.tobygundry.com/logging-front-end-errors-with-your-usual-codeigniter-logging/">Toby Gundry's</a> post on the same technique, but adapted for logging jQuery ajax errors (although I added a few extra things too).<br /><br />In your Javascript:<br /><br />&nbsp; &nbsp;&nbsp;$(document).on({<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; ajaxError: function (event, jqXHR, ajaxSettings) {<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; var err = "Location: " + document.location.href + "; ";<br />&nbsp; &nbsp;<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; if (jqXHR)<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; {<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; err += "Status: " + jqXHR.status + "; ";<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; err += "Text: " + jqXHR.statusText + "; ";<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; }<br />&nbsp; &nbsp;<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; if (jqXHR.responseJSON) {<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; err += "Message: " + jqXHR.responseJSON.Message + "; ";<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; err += "Stack Trace: " + jqXHR.responseJSON.StackTrace + "; ";<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; }<br />&nbsp; &nbsp;<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; if (ajaxSettings) {<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; err += "Data Sent: " + ajaxSettings.data + "; ";<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; err += "URL: " + ajaxSettings.url + "; ";<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; }<br />&nbsp; &nbsp;<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; var message = btoa(err);<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; var log = new Image();<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; log.src = "/JSLogger.ashx?error=" + message;<br />&nbsp; &nbsp;<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; //display some kind of friendly error message to the user<br />&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; }<br />&nbsp; &nbsp; });<br /><br />I used the btoa function for base64-encoding the content, but it's quite possibly unnecessary. &nbsp;Anyway, make a JSLogger handler, something like this:<br /><br />&nbsp; &nbsp; public class JSLogger : IHttpHandler<br />&nbsp; &nbsp; {<br />&nbsp; &nbsp; &nbsp; &nbsp; private static readonly ILog Log = LogManager.GetLogger(typeof(JSLogger));<br /><br />&nbsp; &nbsp; &nbsp; &nbsp; public void ProcessRequest(HttpContext context)<br />&nbsp; &nbsp; &nbsp; &nbsp; {<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; string encodedError = context.Request.QueryString["error"];<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; byte[] bytes = Convert.FromBase64String(input);<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; string error = Encoding.ASCII.GetString(bytes); //using Unicode seems to have weird effects<br /><br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; try<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; {<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; string name = "Username: " + context.User.Identity.Name;<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; error += name;<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; catch(Exception e){} //in case the username isn't available<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Log.Error(error);<br />&nbsp; &nbsp; &nbsp; &nbsp; }<br /><br />&nbsp; &nbsp; &nbsp; &nbsp; //IHttpHandler boilerplate omitted<br />&nbsp; &nbsp; }<br /><br />Let me know if you have any ideas for improvement!