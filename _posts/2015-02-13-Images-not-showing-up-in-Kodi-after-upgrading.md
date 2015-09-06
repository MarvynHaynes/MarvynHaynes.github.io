---
layout:     post
title:      Images not showing up in Kodi after upgrading
date:       2015-02-13 15:08:01
summary:    Images not showing up in Kodi after upgrading.
categories: Kodi
author:     Marvyn
thumbnail: cogs
tags:
 - kodi
 - mySQL
---

Recently I've finally made the update from XBMC Gotham 13.2 to Kodi Helix, but did not come without its issues.  While finalizing my setup, I noticed my some of my imported movies and tv-shows were missing banners, fanart and thumbnails.  Prior to the upgrade, all images were showing correctly and all of my tv/movies folders contain images used by XBMC/Kodi.
<a href="{{ site.baseurl }}/blog_images/AmericanDadScreenshot.png">
	<img src="{{ site.baseurl }}/blog_images/AmericanDadScreenshot.png" alt="Kodi folder structure" width="275">
</a>

My movies and tv-shows plays fine so I knew the main library database was not corrupt.  After a bit of searching I found people with the same issue after performing the upgrade to Kodi.  It seems during the auto migration process, the Textures database that contains information to images gets messed up.  An easy solution for me was to simply delete the Textures13.db file:
#### Linux
`/home/<user>/.kodi/userdata/Database/Textures13.db`
#### Windows
`\Users\<user>\AppData\Roaming\XBMC\userdata\Database\Textures13.db`
#### Mac OS	
`/Users/<user>/Library/Application Support/kodi/userdata/Database/Textures13.db`
#### Andriod	
`/Android/data/org.xbmc.kodi/files/.kodi/userdata/Database/Textures13.db`
#### OpenElec	
`/storage/.kodi/userdata/Database/Textures13.db`

Once the db file is deleted, Kodi will rebuild it as you browse your library and correct the images referencing to the media.
<a href="{{ site.baseurl }}/blog_images/kodi_home.png">
	<img src="{{ site.baseurl }}/blog_images/kodi_home.png" alt="Kodi Home menu" width="275">
</a>

Hope this works for you!