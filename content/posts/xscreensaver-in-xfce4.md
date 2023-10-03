+++
title = 'Xscreensaver in Xfce4'
date = 2023-10-03T19:14:51+01:00
draft = true
tags = [ 'xfce4', 'xscreensaver', 'screensaver', 'desktop']
+++

Today when we leave our machines alone for a few minutes without any interaction, or we lock the session, we're usually
greeted with a blank screen, or if the system is configured, maybe a login screen with a pretty background or some 
corporate styling. Today I want to show you how to install and configure [XScreenSaver](https://www.jwz.org/xscreensaver/) 
to work with the [Xfce](https://www.xfce.org/) desktop environment.

## Installing the necessary packages
This guide assumes you are already running an Xfce desktop, if not, please consult your distro's documentation for 
instructions on how to install it and have it run on boot. I'm using Atch Linux (btw,...) so although the exact instructions
for installing packages might be different for you, you should be able to get the general idea of what is happening.

Firstly, we need to install XScreensaver

```
$ sudo pacman -S xscreensaver
```

After we have installed the XScreensaver package, we need to configure Xfce to start xscreensaver instead of xfce4-screensaver
when the system starts.

## Configuring XFCE
Once the XScreensaver package is installed, we need to head over to the `xfce-settings` application, and scroll to the bottom
of the window until you see the `Sessions & Startup` option.
<br><br/>
{{<figure src="/images/xfce_settings.png" >}}
<br><br>
This will bring up a new window that shows us what applications and services are started when you first login to your Xfce session.
In this screen, make sure you're on the `Application Autostart` tab, and check the box next to *Screensaver (Launch screensaver and locker program)*,
also make sure you uncheck the *Xfce Screensaver* program to make sure that only one
screensaver program is running at any one time.

{{< figure src="/images/xfce_startup.png" >}}

At this point, its best to restart your machine, so that the system can start the correct screensaver service.

## Configuring XScreensaver
One you've rebooted and logged back into your account, you can configure XScreensaver by choosing the option
from the Xfce Application menu
{{<figure src="/images/menu.png" >}}

Clicking on this will bring up XScreensavers control window, where you can choose to have one screensaver
running at a time, or cycle through every 10 minutes (or how ever long you want). You can configure things like timeout, lock settings,
and for some screensavers, you can configure what it displays (from text files, videos etc).
{{<figure src="/images/xscreensaver.png" >}}


