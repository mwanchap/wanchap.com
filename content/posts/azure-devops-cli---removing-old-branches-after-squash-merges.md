+++
title = "Azure Devops CLI - removing old branches after squash merges"
date = 2019-10-15T18:27:00Z
updated = 2019-10-15T18:29:40Z
tags = ["Powershell", "Azure Devops", "git", "CLI"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

We had a git repo with hundreds of already-merged branches which I wanted to clean up.&nbsp; They'd all been merged via "squash merges", meaning there was no merge commit to easily link back to the source branches.  I wanted to delete these unnecessary branches, but only the ones that had definitely already been merged into the master branch via a pull request (PR). Below is how I used the <a href="https://github.com/Azure/azure-devops-cli-extension">Azure Devops CLI</a>&nbsp;to get a list of them. It hinges on the fact that each PR contains the name of the source branch that was being merged at the time.<br /><br /><pre># first, get a list of branches (aka references)<br />$refs = (az repos ref list | convertfrom-json); $refNames = ($refs | select -ExpandProperty name)<br /><br /># next, get a list of all completed pull requests that merged into the master branch<br />$prs = (az repos pr list --status=completed --target=master | convertfrom-json)<br /><br /># finally, find the PRs where the source branch matches one of the current branches, and select some relevant fields. These should be safe to delete<br />$prs | where { $refNames -contains $_.sourceRefName } | select pullrequestid, title, sourceRefName, targetRefName, @{Name="createdBy";Expression={$_.createdBy.uniqueName};}<br /></pre>
