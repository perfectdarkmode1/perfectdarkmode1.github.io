```
title: "Fedora Silverblue"
date: 2023-11-06T06:20:36-07:00
draft: false
```
Automated setup https://universal-blue.org/

You get all the benefits of using containers
Separates system level packages from applications.

System Level
- Desktop, kernel?
- Layering
	- Apps at system level because containers aren't as developed yet
	- Locks to the fedora version you are on

## Layered package examples
	- gnome shell extensions
	- distrobox

![](Pasted%20image%2020230718045403.png)

Uses rpm-ostree?

Flatpacks

Remove fedora flatpack stuff and use flathub repos instead https://flatpak.org/setup/Fedora

Systemd unit for automatic flatpack updates

![](Pasted%20image%2020230718045927.png)

Update every 4 hours to mirror ubuntu

flatseal
adjust permissions of flatpacks

check out apps.gnome.org