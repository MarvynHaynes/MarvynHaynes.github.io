---
layout:     post
title:      No Stereo Mixer
date:       2013-09-06 17:06:14
summary:    No Stereo Mixer.
categories: Windows
author:     Marvyn
thumbnail: cogs
tags:
 - Windows
 - Hardware
---

I wanted to blog this issue I had a few days ago before I forgot.

I needed to figure out how to record some audio clips from youtube using the same PC.  We have 3 popular options:
 

**1. Male to Male headphone cable**

<img src="http://img.alibaba.com/photo/11730506/Audio_Extension_Cable.jpg" alt="Male to Male headphones" width="200">
 
Plug 1 end to of the cable to the 'audio out' and the other end to 'line-in' on your soundcard.  Adjust volume as necessary.

**2. Enabling Stereo Mix option (Windows 7 users)**

![Enabling Stereo Mix](http://www.howtogeek.com/wp-content/uploads/2010/12/stereo_mix_03.png "Sound options")

By enabling the hidden Stereo Mix option under Recording Devices, it should allow you to record any playback on your computer.  For a step by step guide, check How To Geek's guide: [How To Enable “Stereo Mix” in Windows 7 (to Record Audio)](http://www.howtogeek.com/howto/39532/how-to-enable-stereo-mix-in-windows-7-to-record-audio/)
 

**3. Using 3rd party apps**

![Using 3rd party apps](http://www.freesoundrecorder.net/img/demo.png "Third Party Apps")


There are a few 3rd party apps specifically made for recording audio that comes out of your PC, some better than others, such as [AV-Replay](http://www.replay-av.com/) and [Freecorder](http://freecorder.com/).  Personally I'm cautious of installing these types of apps, so read reviews before downloading.

You can find a comprehensive list from the [stream-recorder.com](http://stream-recorder.com/forum/audio-video-recording-software-allows-record-sound-t5839.html?t=5839) forums

**<u>Problem</u>**:
I opted for choice #2 as I didn't have a free male to male cable and didn't want to install any 3rd party apps.  The issue I had is after selecting '*show disabled devices*' the stereo mix icon was <u>still not there</u>.

**<u>Solution</u>**:
Reinstall your soundcard drivers via your manufacturer website.  When I originally installed Win7 I opted to use the soundcard drivers the windows update service provided to me and it seemed to work well.  Little did I know, the updates are known to remove the stereo-mix option and it has been suggested Microsoft purposely does this because of [Microsoft’s DRM (Digital Rights Management)](http://faph.wordpress.com/2008/09/01/audacity-vista-stereo-mix-gone/).

In any case, once after I reinstalled my drivers from my manufacturer (onboard soundcard from MSI aka RealTek) and a reboot, the Stereo-Mix option is now viewable and ready to use.