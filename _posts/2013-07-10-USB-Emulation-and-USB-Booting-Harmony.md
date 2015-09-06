---
layout:     post
title:      USB Emulation and USB Booting Harmony
date:       2013-07-10 20:15:46
summary:    USB Emulation and USB Booting Harmony.
categories: Windows
author:     Marvyn
thumbnail:  cogs
addCSS:		myCustom.css
tags:
 - Windows
---

Last week I spent the full 5 days trying to install Windows 7 and have my PC be able to dual boot with Ubuntu 11.10 ([XBMCbuntu](http://wiki.xbmc.org/index.php?title=XBMCbuntu)).

To say the least, for such a simple task it was a very long and tiring journey. Obstacle over obstacle, I conquered one after the next, some took a few hours, others a couple of days.  Yet Google was with me throughout my time of difficulty.

<div class="thumbnail with-caption">
  <img src="https://ponyinthepasture.files.wordpress.com/2011/11/is-google-god.jpg?w=240">
  <p>Praise be to Google.</p>
</div>

What I wanted to share was an issue I actually came across a long while back when I first installed XBMCbuntu from my 1GB USB key.

**Problem**: Your computer does not boot up any USB key that is 2GB or lower. Seems to ignore the USB key and boots up Hard drive as normal.
 
As a quick rundown,  normally when you want to bootup your PC from USB key to run a different O/S or installation you would follow the 3 general rules:
* Format USB key.
* Transfer boot able ISO(s)/Files to USB key using special software that would also make USB key boot able.
* Alter the bootup sequence either by bringing up boot device menu (after POST test) or in BIOS itself.

But the USB key still was not booting.

What gives?

**Answer**:  Switch the USB Storage Emulation to Hard Disk (*applies to usb keys 2GB and lower*)
`Enter BIOS` -> `Intergrated Prepherials` -> `USB Storage Emulation` -> `Select Hard Disk`


<a href="http://3.bp.blogspot.com/-uRBuqKAE4DQ/UBNRnBFdO8I/AAAAAAAAA_U/9ert8jfPtmY/s1600/IMG_20120727_222540.jpg">
	<img src="http://3.bp.blogspot.com/-uRBuqKAE4DQ/UBNRnBFdO8I/AAAAAAAAA_U/9ert8jfPtmY/s1600/IMG_20120727_222540.jpg" width="240">
</a>

This setting forces BIOS to recognize USB Drives under 2GB as bootable hard drives.  If selected  as Auto or Floppy, the machine will treat the USB key has a floppy drive.  While I haven't had a chance to fully understand why this feature is needed in BIOS, I can say that majority of users that come across this issue are owners of Acer Computers ([via google search](https://www.google.ca/search?hl=en&q=%22usb+storage+emulation%22+bios&ei=TbroVaeuIpGXygTW24jIBg)) but it is possible users of other Manufactures  can come across the same issue.

Keep in mind I am only sharing this because this worked for me.  My machine is an [Acer Revo 3610](http://www.amazon.com/Acer-AspireRevo-AR3610-U9022-Desktop-Dark/dp/B0030L3ASU) that I use as a Media PC hooked up to my living room widescreen TV.  If you tried this and still cannot boot up from your USB Key you might want to try the same key on a different machine to isolate the issue.