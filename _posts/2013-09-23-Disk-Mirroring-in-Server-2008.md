---
layout:     post
title:      Disk Mirroring in Server 2008
date:       2013-09-23 11:45:23
summary:    Disk Mirroring in Server 2008.
categories: Windows Server
author:     Marvyn
thumbnail:  cogs
addCSS:		myCustom.css
tags:
 - Windows Server
---

I just wanted to add yet another quick reminder, this time a feature in Windows Server 2008.  One of my buddies is just starting to implement his server at home and I advised him of a quick contingency feature of Server 2008 that I myself have used in the past.

[Configuring Disk Mirroring for Windows Server 2008 R2](http://www.microsoft.com/en-us/download/details.aspx?id=23476)

Now there are countless amount of guides on the net on how to set this up, so I wont go into detail about the steps but I will provide the reason why was ideal for me.

* It's Easy
* It's Fast
* No 3rd party apps needed 
* No special hardware needed
* Once setup, I dont have to tinker around with it again. (Unless the Hard drive fails)

And of course, I looked at the cons:

* It mirrors everything on your original hard drive, including any possible corrupted files, viruses or bad configurations.
* Since the server has to write data to 2 different hard drives, performance will be affected.
* The backup drive is used just as much as the Primary drive (due to mirroring data)

<a href="http://4.bp.blogspot.com/-qGVz2dCkWxU/UAN0968rDOI/AAAAAAAAA7Q/mQ8u4dkj_WM/s200/backups.jpg">
	<img src="http://4.bp.blogspot.com/-qGVz2dCkWxU/UAN0968rDOI/AAAAAAAAA7Q/mQ8u4dkj_WM/s200/backups.jpg" width="300" class="pull-right">
</a>
I understand and I **do** agree; for alot of people, this is not the ideal backup plan (*The first 2 cons are usually a deal breaker for most*). Personally, it was a time where I was just getting myself up and running Server 2008 and needed to have some sort of redundancy up for the O.S drive asap. Once I was up and running after a little while long while, I had time to tinker around with other features and do my research into what 3rd party app I could look into for backup. I'm currently fiddling with [Symantec Backup Exec](http://www.symantec.com/backup-exec) but I feel this far exceeds my average backup needs.

 

I hope this quick article gives someone a better idea on what route they do plan to follow in their contingency plan. Here are some more links for those who are interested in setting up different RAIDs in Server 2008.

* [TheGeekStuff - RAID 0, RAID 1, RAID 5, RAID 10 Explained with Diagrams](http://www.thegeekstuff.com/2010/08/raid-levels-tutorial/)
* [Techotopia - Creating and Managing Windows Server 2008 Striped (RAID 0) Volumes](http://www.techotopia.com/index.php/Creating_and_Managing_Windows_Server_2008_Striped_(RAID_0)_Volumes)
* [Techotopia - Configuring Disk Mirroring (RAID 1) on Windows Server 2008](http://www.techotopia.com/index.php/Creating_and_Managing_Windows_Server_2008_Mirrored_(RAID_1)_Volumes)
* [Mirroring Windows Server 2008 GBT and MBR Boot and System Disks](http://www.techotopia.com/index.php/Mirroring_Windows_Server_2008_GBT_and_MBR_Boot_and_System_Disks)
* [Techotopia - Configuring and Managing RAID 5 on Windows Server 2008](http://www.techotopia.com/index.php/Creating_and_Managing_Windows_Server_2008_Striped_(RAID_0)_Volumes)

I would like to hear from any readers out there.  If you do have a backup method, what program or tools do you use and why does it work for you?
<a href="http://2.bp.blogspot.com/-TYPjnrxNFms/UANztgz9DnI/AAAAAAAAA7I/aVHBQNjR6XY/s320/noah-backup.jpg">
	<img src="http://2.bp.blogspot.com/-TYPjnrxNFms/UANztgz9DnI/AAAAAAAAA7I/aVHBQNjR6XY/s320/noah-backup.jpg" width="300">
</a>