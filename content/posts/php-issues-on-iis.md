+++
title = "PHP Issues on IIS"
date = 2017-02-20T17:58:00Z
updated = 2017-02-20T17:58:52Z
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

PHP ignores the application pool user setting and runs as IUSR<br /><br />Debugging:<br />echo get_current_user();<br />&nbsp; &nbsp; ini_set('display_errors', 1);<br />&nbsp; &nbsp; ini_set('display_startup_errors', 1);<br />&nbsp; &nbsp; error_reporting(E_ALL);
