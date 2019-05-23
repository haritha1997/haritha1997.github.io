---
layout: post
title: How to Solve Realtek Wifi Issue in Ubuntu and Arch Linux
description: >
  A tutorial to solve low range wifi issue during new installation or upgradation of Ubuntu and Arch Linux.
image: /assets/img/wifiissue.jpg
noindex: true
---
Ever experienced a weak wifi signal, which disconnects as you move your laptop away, when you recently installed your operating system? Didn't find the list of wifi connections in the wifi menu? Don't worry, you're in the right place.!

From my personal experience, I've always encountered this wifi issue as I try out a new operating system or upgrade the existing one on my system. It shows a weak signal and doesn't list all the nearby available wifi connections in the wifi menu. And I know, it's really tedious to install all your files and libraries with a weak signal, which just breaks off as you switch to another room from the router, or that connects only on a hotspot. Frustrating.

On the go, I realized it's because some of the files regarding my Realtek wifi driver (RTL8723be) is missing and installing it solves the issue. This problem occurs because the network hardware is using the wrong antenna for communication.

I've been an ardent user of Arch Linux and Ubuntu, but the installation for this on these two operating systems are different. This article will guide through fixing your wifi in Arch Linux and Ubuntu distributions.

# In Ubuntu

## Download WiFi driver source files:

Establish a network connection by using an Ethernet cable from your router or turn on your mobile hotspot placed near to your system to download the necessary files. Download the zip file from the below link, unzip it, and copy the files onto the Desktop for easy accessibility.  To download the zip file: [Download](https://github.com/lwfinger/rtlwifi_new.git)

 
## Open the Terminal:

Type in the following commands.

```
 cd rtlwifi_new
```

Now the directory is changed to the required driver file folder. In order to build and install the components in the driver file, type in the following.

```
 make
```
Wait for the processes to get finished. Enter the sudo commands below and give the necessary authentication password wherever required. Please note that rtl8723be is the name of my wifi driver. You can find yours by running the *lspci* command on the terminal. 
 
```
sudo make install 
sudo modprobe -rv rtl8723be 
sudo modprobe -v rtl8723be ant_sel=2
```

Enter the *iwconfig* command, and note down the id displayed at first starting with “wl___”. Keep that id in mind to use it and replace your corresponding id( depends on the network card that each user is using) in the place of the code starting with “wl” in the following commands.

```
sudo ip link set wlo1 up 
sudo iw dev wlo1 scan
```

To make your settings permanent,

```
`echo "options rtl8723be ant_sel=2" | sudo tee /etc/modprobe.d/50-rtl8723be.conf``
```
# In Arch Linux

In any Arch Linux distro, I myself used Antergos, the scenario is quite different from Ubuntu. Arch Linux has the RealTek Wifi Driver files already installed, only issue was the antennae selection by the network hardware was wrong. So, removing the package and re-installing with the proper antennae selection solved the issue.! Type in the following commands if you find the same difficulty:

## Open the Terminal:

Type in the following commands.

```
sudo modprobe rtl8723be -r
sudo modprobe rtl8723be ant_sel=2
``` 

And that should get everything working! 🙂
