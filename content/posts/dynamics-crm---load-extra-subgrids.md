+++
title = "Dynamics CRM - Load extra subgrids"
date = 2014-07-13T23:14:00Z
updated = 2014-07-13T23:14:50Z
draft = true
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

CRM update changed the page loading somehow so that subgrid rendering is deferred until after the Form OnLoad event fires.<br /><br />Previous solution here<br />http://blog.customereffective.com/blog/2011/12/crm-2011excessive-sub-gridding.html<br /><br />No longer works, as the&nbsp;ms-crm-List-LoadOnDemand elements don't exist yet. If you put a breakpoint on your OnLoad code in the browser dev tools and try to dig inside one of the subgrids, you'll notice that there's an empty div in there with an ID like "SubGridName_crmGridTD". &nbsp;If you resume script execution while watching the DOM, you'll notice that this div only becomes populated once OnLoad finishes. &nbsp;So in order to make Paul's code work, it needs to be deferred further by wrapping the lot in a setTimeout, like so:<br /><br />setTimeout(function () {<br /><span class="Apple-tab-span" style="white-space: pre;"> </span>var lnksUnloaded = getLinksWithClassName('ms-crm-List-LoadOnDemand');<br /><span class="Apple-tab-span" style="white-space: pre;"> </span>for (var i = 0; i &lt; lnksUnloaded.length; i++){<br />&nbsp; &nbsp;<span class="Apple-tab-span" style="white-space: pre;">  </span>lnksUnloaded[i].click();<br /><span class="Apple-tab-span" style="white-space: pre;"> </span>}<br />}, 1000);<br /><br />You can change the timeout duration to whatever you like, I left it at 1 second since CRM can be a little slow sometimes, so your mileage may vary. &nbsp;This is a bit of a hack and there's perhaps a much easier way to do it. Also, the code can be neatened up a bit if you're already using jQuery (as I am) by replacing Paul's code with:<br /><br />setTimeout(function () {<br /><span class="Apple-tab-span" style="white-space: pre;"> </span>$(".ms-crm-List-LoadOnDemand").each(function(){this.click();});<br />}, 1000);<br /><br />
