---
title: Disable Gatekeeper & Install Apps from anywhere
date: '2016-06-06 00:00:00'
layout: post
tags:
- macOS
- Sierra
categories: Apple
no-post-nav: true
---

With macOS Sierra, the usual option to allow apps downloaded from anywhere is now disabled. It is not visible from System Preferences at the moment so the only way to activate it is through Terminal. It worth pointing out that this is only a beta relase and this may change overtime or be added back to System Preferences. There has been some discussion on Twitter from Apple engineers that state this is actually a bug and not the way macOS Sierra is intended to deal with unsigned apps from outside the mac AppStore. 

To enable 'install apps from anywhere' simply copy and paste the below code into the terminal. To load terminal pres CMD + Spacebar and type terminal and click enter. Then simply copy and paste and enter your password when prompted. 

`sudo spctl --master-disable`

That's it. Happy installing! 
