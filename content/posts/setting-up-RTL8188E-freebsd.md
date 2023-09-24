+++
title = 'Setting Up A Wireless USB Network Card In FreeBSD'
date = 2023-09-24T15:22:23+01:00
description = 'Setting up a TP Link TL-WN725N USB wireless adapter on FreeBSD. This is a walkthrough guide for installing the adapter based on the RTL8188EU network device.'
comments = true
tags = [ 'FreeBSD', 'wifi', 'networking', 'TP Link', 'TL-WN725N' ]
image = '/images/wifi.jpg'
draft = false
+++
## Introduction

Recently I bought a TP Link USB adapter, TL-WN725N which is based around the RTL8188EU network
device. I wanted to enable Wifi on my laptop where the wifi card was not supported under
FreeBSD. What follows are the steps I took to enable it on my laptop (an old Dell Inspiron 3000).
 
I wrote this handy guide mainly for my future self, knowing that at some point in the future I'll be 
scratching my head trying to figure out how do I get the WiFi working on a BSD box again!


### Notes
This guide is written for the ```rtwn``` driver for the RealTec RTL8188E(U) card and similar, and
is being installed on a system with FreBSD-13.2-RELEASE, with all patches and updates applied.

As we'll be editing system files, remeber to either login as root or prepend the commands with
either ```doas``` or ```sudo``` depending on which is installed on your system.

### Step 1

Firsty we need to create the wireless Device by running

```
ifconfig wlan create wlandev rtwn0
```

Then add the following code to ```/etc/rc.conf```:

```
wlans_rtwn0="wlan0"
```

### Step 2
Next we need to add the details about the wireless network we want to connect to, to the
```/etc/wpa_supplicant.conf``` file. If it doesn't exist, then create it. Append the following
to the end of the file:

```
network={
    ssid="MYROUTERNAME"         # Replace with your routers SSID
    psk="VerySeceretPassword"   # Replace with your router WPA key
}
```

Once you've added this, run the following command to check it's working ok, and that no errors
are reported

```
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf
```

As long as no errors are reported, ```ctrl-c``` to break out in the terminal, ready to complete
the setup.

### Step 3
Now that the WiFi credentials have been saved and no errors have been reported, we need to tell
the system how to connect - in this case, we're using WPA authentication and SYNCDHCP to get
our IP address and DNS server info from the router.
Add the following to your ```/etc/rc.conf``` file to persist across reboots:

```
ifconfig_wlan0="WPA SYNCDHCP"
```

Save the file, and then run the following command in the terminal to restart networking. After
this command is run, you should find that your WiFi is connected.

```
service netif restart
```

### Conclusion
Hopefully by following the above steps, you should have a fully working wifi connection on
your box. These instructions can be replicated for other wifi cards by replacing the
```rtwn0``` text where it appears in the code blocks with the name of the driver for the
card you are trying to use (assuming that there is a driver for your card and it is available
for the version of FreeBSD you are using).



