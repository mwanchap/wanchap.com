+++
title = "Dynamics CRM - Replacing old CRM 4 API references with regular expressions"
date = 2014-02-19T21:19:00Z
updated = 2014-02-19T21:20:07Z
tags = ["Regular Expressions", "Dynamics CRM 2011"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

When upgrading Dynamics CRM 2011 to the most recent set of updates, it turns out that CRM 4 API stuff was no longer supported, even though the Microsoft code validation tool said that it should all work in IE! &gt;:-[<br /><div>So I needed to quickly replace loads of old CRM 4 API references, such as<br /><br /><span style="font-family: Courier New, Courier, monospace;"><span class="Apple-tab-span" style="white-space: pre;"> </span>crmForm.all.some_field.DataValue = 1;</span><br /><br />with the newer CRM 2011 API, which in this example would look like:<br /><br /><span style="font-family: Courier New, Courier, monospace;"><span class="Apple-tab-span" style="white-space: pre;"> </span>Xrm.Page.getAttribute("some_field").setValue(1);</span><br /><br />We had thousands of these scattered all throughout about over 50 javascript files from long ago, back when we were running CRM 4, and many of them hadn't been updated with the new API. This would have been extremely laborious if it were not for a couple of pretty handy regular expressions I came up with (plus a bit of help from my colleague to perfect the first):<br /><br />Find:<br /><br /><span style="font-family: Courier New, Courier, monospace;"><span class="Apple-tab-span" style="white-space: pre;"> </span>crmForm\.(?:all\.|\w*?)(\w*)\.DataValue</span></div><div><span style="font-family: Courier New, Courier, monospace;"><br /></span>And replace with:<br /><br /><span style="font-family: Courier New, Courier, monospace;"><span class="Apple-tab-span" style="white-space: pre;"> </span>Xrm.Page.getAttribute("$1").Value</span></div><div><span style="font-family: Courier New, Courier, monospace;"><br /></span>After that, it's still necessary to replace "Value" with either of the getValue or setValue functions depending on usage, since making a regex that could match all possible usage patterns was way too difficult, and this would have certainly been quicker in the end. It's pretty simple, but it saved a heck of a lot of fiddly copy/pasting work!</div>
