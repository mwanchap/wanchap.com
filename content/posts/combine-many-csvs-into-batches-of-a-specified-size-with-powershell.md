+++
title = "Combine many CSVs into batches of a specified size with Powershell"
date = 2020-03-02T20:39:00Z
updated = 2020-03-02T20:39:27Z
tags = ["Powershell"]
blogimport = true 
[author]
	name = "Matt Wanchap"
	uri = "https://www.blogger.com/profile/16465307324394182190"
+++

<pre>$batchMaxSize = 9.5MB<br />$allFiles = Get-ChildItem 'fileLocation\*.csv'<br />$batchNumber = 0;<br />$batchMagnitude = $allFiles.Count.ToString().Length<br /><br /># group the files together until there's none left<br />while ($allFiles.Count -gt 0) {<br />    $batchNumber++;<br />    $batchSuffix = $batchNumber.ToString().PadLeft($batchMagnitude,"0");<br />    $totalSize = 0;<br /><br />    # add the file sizes together, keeping a running total until it exceeds the max<br />    $batchFiles = $allFiles | where {$totalSize += $_.Length; $totalSize -lt $batchMaxSize};<br /><br />    # combine the files in memory - don't need to deal with headers<br />    # this step could cause memory issues with extremely large files<br />    # but then you probably wouldn't be batching them ;)<br />    $comboFile = $batchFiles | Foreach-Object {<br />        Import-Csv -Path $_;<br />    }<br /><br />    $comboFile | Export-Csv "batched\batch-$batchSuffix.csv" -Encoding ASCII -NoTypeInformation<br /><br />    # removes the files we just batched together from the list of all files<br />    $allFiles = (Compare-Object $allFiles $batchFiles).InputObject<br />}<br /></pre>
