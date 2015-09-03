---
layout:     post
title:      Deleting Recovery Partition
date:       2013-08-14 15:02:06
summary:    Solving the greyed out menu options while trying to delete the recovery partition.
categories: Windows
author:     Marvyn
thumbnail: cogs
tags:
 - Windows
 - Disk Management
---

Today I was preparing an old hard drive for data backup when I had problems deleting 1 of its partitions.  I normally use Disk Management under Control Panel -> Computer Management however when I right clicked on the partition everything is greyed out except the help item.
<a href="http://www.winability.com/info/delete-partition/disk-management-menu-disabled.png">
	<img src="http://www.winability.com/info/delete-partition/disk-management-menu-disabled.png">
	<div class="caption">
		<p>The above image is not a screenshot of my pc but reflects the same issue.</p>
	</div>
</a>

Because this hard drive used to belong to store bought laptop, it came with a recovery partition that is by default hidden and possibly write protected, which is the norm for most laptops today (along with bloatware).  I found this simple solution via sevenforums.com which hopefully helps others as it did for me quickly:

* Go to command prompt
* Type diskpart

Enter the following:

* `diskpart`
* `list disk`
* `select disk [yourDiskNumber]` (e.g. your disk is #5 type: `select disk 5`)
* `list partition`
* `select partition [yourParitionName]` (e.g. partition name is recovery: `select partition recovery`)
* `delete partition override`
 
<a href="http://www.lacie.com/imgstore/LaBrain/lb-xp_diskpart_3%5B1%5D1.jpg">
	<img src="http://www.lacie.com/imgstore/LaBrain/lb-xp_diskpart_3%5B1%5D1.jpg">
	<div class="caption">
		<p>Not my screenshot, just an example what to look for.</p>
	</div>
</a>

A thorough guide on how to use diskpart commands you can find [here](http://support.microsoft.com/kb/300415).

This worked wonderful for me. It was quick and easy and no extra 3rd party software was needed.  Of course this will work with any of the O.S that has the diskpart utility (Windows 7, Server 2008, etc) so Win XP users or lower may have to use a utility like Partition Magic or [Partition Wizard](http://www.partitionwizard.com/free-partition-manager.html).  I also wanted to note since this was a secondary drive I was using, I did not have to boot into Win 7 recovery mode to make any changes as some people might need to if this is their boot drive they are working on.

You can read the full thread on sevenforums.com [here](http://www.sevenforums.com/installation-setup/67944-can-i-delete-healthy-recovery-partition.html).