---
layout: post
title: How to Solve Realtek Wifi Issue in Ubuntu and Arch Linux
description: >
  A tutorial to solve low range wifi issue during new installation or upgradation of Ubuntu and Arch Linux.
image: /assets/img/blog/example-content-ii.jpg
noindex: true
---

New to Ubuntu? Or recently installed Ubuntu on your device?  upgraded to latest version 16.04 LTS ?? are some of the questions that arouse in a tech geek’s mind when the not-so-geeky people complain that their laptops are not showing the available WiFi networks in the area or have connections with very poor range when they log into Ubuntu. Over the time it has been a very common issue for all the Linux users, especially the newcomers.

From  personal experience, the following steps have proven useful when the WiFi hardware in my device was showing poor range(can be accessed only in a position very close to the router) and no other networks were detected. This is because your network hardware is using the wrong antenna configuration for communication.


## Solution :


## Download WiFi driver source files:

Establish a network connection by using an Ethernet cable from your router to download the necessary files. Download the zip file from the below link, unzip it, and copy the files onto the Desktop for easy accessibility.  To download the zip file: [Download](https://github.com/lwfinger/rtlwifi_new.git)

 
##  Open the Terminal:

Type in the following commands.

```
cd Desktop cd rtlwifi_new-rock.new_btcoex
```

Now the directory is changed to the required driver file folder. In order to build and install the components in the driver file, type in the following.

```
`make`
```
Wait for the processes to get finished. Enter the sudo commands below and give the necessary authentication password wherever required.
 
```
sudo make install sudo modprobe -rv rtl8723be 
sudo modprobe -v rtl8723be ant_sel=2
```

Enter the iwconfig command, and note down the id displayed at first starting with “wl___”. Keep that id in mind to use it and replace your corresponding id( depends on the network card that each user is using) in the place of the code starting with “wl” in the following commands.

```
sudo ip link set wlo1 up 
sudo iw dev wlo1 scan
```

To make your settings permanent,

```
`echo "options rtl8723be ant_sel=2" | sudo tee /etc/modprobe.d/50-rtl8723be.conf``
```
And that should get everything working! 🙂
