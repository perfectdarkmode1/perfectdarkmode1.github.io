---
title: "Distrobox Guide"
date: 2023-11-06T06:20:36-07:00
draft: false
---

Github: https://github.com/89luca89/distrobox


Run native containers that have access to the host file system
Creates an app launcher icon for the container

Launch gui apps from other distros natively. Even without spinning up the container first

Make separate shortcuts for separate distros in the terminal

Make a profile in the terminal for the container:

`distrobox-enter --name ubuntu-20

Make sure to check the box "run a custom command instead of my shell"

Then set a custom shortcut in your OS to that terminal profile
`gnome-terminal --profile=ubuntu`

## How to Install

`curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/install | sudo sh`

or 

`sudo dnf -y install distrobox`

You can find a list of container distros here: https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#host-distros

## Commands

### Create a container
`distrobox create --name aur --image archlinux` or
`distrobox-create --name archlinux --image docker.io/library/archlinux` or
`distrobox create -n ubuntu -i ubuntu:20.04`

### Additional Options

--nvidia
	- add your host nvidia drivers

--additional-packages {package-name}
	- install additional packages

### Enter the container

`distrobox enter aur`

### Add app from another distro to your app launcher/ application menu

`distrobox-export --app app-name 

### Create a GUI app 

`distrobox-export --app {appname}`

Create a temporary container
distrobox-ephemeral --image archlinux

Create a container for testing server distros
`distrobox create --image almalinux:latest`

Create an arm container
```
distrobox create -i aarch64/fedora -n fedora-arm64
distrobox enter fedora-arm64
```

Add distro to your display manager to boot into the distribution

https://cloudyday.tech.blog/2022/05/14/distrobox-is-awesome/
https://github.com/89luca89/distrobox/blob/main/docs/posts/run_latest_gnome_kde_on_distrobox.md


