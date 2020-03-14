+++
title = "'A section using configSource may contain no other attributes or elements' error after installing Application Insights"
date = 2018-05-03T23:45:00Z
updated = 2020-03-13T22:44:42Z
tags = ["Umbraco", "ASP.NET", "Application Insights"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

After installing the Application Insights nuget package to an Umbraco solution, you'll get this error:<br /><br />A section using 'configSource' may contain no other attributes or elements<br /><br />&lt;ExamineLuceneIndexSets configSource="config\ExamineIndex.config" /&gt;<br />&nbsp; &nbsp; &nbsp;&lt;log4net configSource="config\log4net.config"&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&lt;root&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&lt;level value="ALL" /&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&lt;appender-ref ref="aiAppender" /&gt;<br />Source File: \project\web.config<br /><br />This happens because part of the Application Insights installation process adds a &lt;log4net&gt; section to web.config.&nbsp; Which would make sense, except Umbraco already has a &lt;log4net&gt; section in /config/log4net.config.&nbsp; So as you can imagine, the solution is to manually move everything its added into that file. Unfortunately you can't just copy/paste the whole lot, but it's not particularly complicated:<br /><br /><br /><ol><li>Move &lt;appender-ref ref="aiAppender" /&gt;&nbsp;into the log4net.config file's &lt;root&gt; node</li><li>Move the &lt;appender name="aiAppender" ...&gt; section underneath the existing appenders in log4net.config</li><li>Back in web.config, change the &lt;log4net&gt; section back to what it was before.</li></ol><br /><br />
