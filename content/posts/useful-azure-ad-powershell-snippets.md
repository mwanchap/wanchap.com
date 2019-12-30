+++
title = "Useful Azure AD Powershell snippets"
date = 2019-04-14T18:30:00Z
updated = 2019-10-17T18:37:07Z
tags = ["Active Directory", "Azure", "Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

I've been doing a lot of Azure AD stuff lately, so here are some powershell snippets that have been coming in handy.<br /><br />I always forget to&nbsp;<code>Connect-AzureAD</code> first, so don't do that<br /><br /><h3>Get extension properties of a user (e.g. created date)</h3><br /><code>Get-AzureADUser -SearchString 'username or email addy' | select -ExpandProperty ExtensionProperty</code><br /><br /><h3>Get guest users that are not members of a specified group</h3><br /><code>$allGuests = Get-AzureADUser -Filter "usertype eq 'guest'" -All $true<br />$groupMembers = Get-AzureADGroup -SearchString 'group-name' | Get-AzureADGroupMember -All $true<br />$allGuests | where {$groupMembers -notcontains $_ }</code><br /><br /><h3>Guest users that have not accepted their invitations to join Azure AD</h3><br /><code>Get-AzureADUser -Filter "usertype eq 'guest'" -All $true | where UserState -eq PendingAcceptance</code><br /><br /><h3>Add a big list of users to a group</h3><div>Assuming all the usernames are in a text-file, one line each:<br /><br /></div><div><code>$group = get-azureadgroup -SearchString "group name"<br />get-content .\users.txt | % { $user = Get-AzureADUser -SearchString $_; Add-AzureADGroupMember -ObjectId $group.ObjectId -RefObjectId $user.ObjectId }</code><br /><br /><h3>Turn off password expiry (e.g. for a service account)</h3></div><div><code>Set-AzureADUser -ObjectId $user.ObjectId -PasswordPolicies DisablePasswordExpiration</code></div><div><br /></div><div><br /></div>
