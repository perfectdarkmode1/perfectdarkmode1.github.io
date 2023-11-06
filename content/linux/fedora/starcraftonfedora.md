```
title: "How to Install Starcraft on Fedora"
date: 2023-11-06T06:20:36-07:00
draft: false
```
https://www.youtube.com/watch?v=eefsL9K2w4k

# Starcraft 2 install on Fedora Workstation 38


## Install your latest gpu driver https://github.com/lutris/docs/blob/master/InstallingDrivers.md

I am just running off of built in AMD graphics. So we just need to install support for Vulkan API
`sudo dnf install vulkan-loader vulkan-loader.i686`


Install Wine
`$ sudo dnf -y install wine`

Install Lutris
Install the Flatpak version in software center.