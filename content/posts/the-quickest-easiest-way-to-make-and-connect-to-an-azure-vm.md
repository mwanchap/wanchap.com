+++
title = "The quickest, easiest way to make and connect to an Azure VM"
date = 2019-08-15T23:27:00Z
updated = 2019-10-24T22:41:32Z
tags = ["Azure", "Powershell", "CLI"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

Connect-AzureRmAccount<br />$creds = Get-Credential<br />$vmname = "TestVM"<br />$vm = New-AzureRmVm -Name $vmname -Credential $creds -Location "AustraliaEast" -Size "Standard_DS3_v2" # obviously change size and location as required<br />$fqdn = $vm.FullyQualifiedDomainName;<br />$username = $creds.UserName;<br />"full address:s:$fqdn" | out-file "~\desktop\$vmname.rdp";<br />"username:s:$vmname\$username" | out-file "~\desktop\$vmname.rdp" -Append;<br /><br />
