---
layout:     post
title:      Installing Drupal and mySQL with Microsoft Web Platform Installer
date:       2013-06-16 17:06:14
summary:    Installing Drupal and mySQL with Microsoft Web Platform Installer.
categories: Drupal
author:     Marvyn
thumbnail: cogs
tags:
 - Drupal
 - IIS
 - mySQL
---

One of the great things about IIS 7.5 is the ease of installing components using the [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx) by Microsoft. It allows you to install IIS extensions, Frameworks, Web Apps and various Tools with a few clicks of a button. So using this app I was able to search for Drupal and install it (You can find a great step-by-step installation guide on [Drupal.org](https://drupal.org/node/1130898).

One of the great things about this app is that it also downloads any additional dependencies needed which in my case it retrieved the latest versions of PHP, Windows Cache Extension for PHP, and mySQL Connector/NET). Since I already had mySQL installed, during the installation I could simply point to it for the Drupal database. Things were going smooth however I came across a slight problem. It seems the Web Platform Installer gave me an error:

> The specified password for user account ‘root’ is not valid, or failed to connect to the database server.

The first thing I checked was to verify mySQL Connector/NET was correctly added as a dependency, which was fine. Then I realized the Web Installer Platform was trying to connect to my existing mySQL database as the user **root** which I changed a while back for security measures.

Unfortunately I could not find any options in the Web Platform setup to change the root username to what I had, so my only option is to go in my database to temporarily switch the root username to the original 'root' name in order to allow installation to continue. Login to your database as your root username and execute the following:

* Connect to the mySQL database: use mysql;
* Change username back to original root:
* update user set user="root" where user="current username";
* Finally, flush cache and commit: flush privileges;

Then I restarted the installation again and was able to install everything successfully. Once that was completed I connected connected back to the mySQL database and re-ran the same code but reverse the usernames. As Developers we have this natural urge to troubleshoot in complexity without taking a moment to think simply so hopefully this helps anyone out there who's experienced similar issues.