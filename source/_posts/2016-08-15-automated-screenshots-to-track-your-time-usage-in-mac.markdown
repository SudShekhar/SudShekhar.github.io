---
layout: post
title: "Automated screenshots to track your time usage in mac"
date: 2016-08-15 14:06:17 +0530
comments: true
categories: mac, shell script, utilities
---

Recently, I was trying to figure out the best way to track how I spend my time while in front of the computer. There are a lot of time tracking softwares available for OSX but it's not easy to find the best ones. Moreover, you might not be allowed to install third-party softwares on an office laptop (or might prefer a more DIY method).

To achieve this, I recently setup a shell script to take automatic screenshots of my screen every 1 minute. This lets me quickly check exactly what I was doing at any specific point of time through out the day. Having a screenshot showing exactly what you were doing also provides more context than merely app name and usage.


## Automating screen shots on mac

+ create a folder called `screenshots` in your home directory
{% codeblock lang:sh %}
mkdir ~/screenshots
{% endcodeblock %}

+ create a script `screenshot.sh` in the home directory. Add the following lines in it.
		
{% codeblock lang:sh %}
#!/bin/sh
fileName=screenCapture #replace with whatever prefix you choose
current_time=$(date "+%Y.%m.%d-%H.%M.%S").jpg #current time in day, minutes with jpg extension
new_file_name=$filename.$current_time # file name where screenshot is stored
/usr/sbin/screencapture -x ~/screenshots/$new_file_name #you need to give full path to screencapture, -x doesn't produce the screen capture sound
{% endcodeblock %}

+ Save the 	file with executable permissions

		chmod +x screenshot.sh

+ Edit your crontab file, `vim /etc/crontab`. As root, add the following line and save it

{% codeblock lang:sh %}
*   *   *   *   *   yourusername     /Users/yourusername/screenshot.sh  >> /tmp/screenshot.log 2>&1
{% endcodeblock %}


And that's it! You should start seeing screenshots being stored in your `~/screenshots/` folder. If it isn't so, checkout the `/tmp/screenshot.log` file for errors generated and fix them.

**Note** : To reduce the frequency of screenshots, just edit the `/etc/crontab` file and update the frequency there.

