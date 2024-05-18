---
title: Switching to Linux
date: 2023-11-06T06:20:36-07:00
draft: true
---
Finding program replacements

Office

Kindle

Cloud reader:

https://read.amazon.com/kindle-library

Calibre:

sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin

Virtual box: https://linuxhint.com/install-virtualbox-linux-mint/

$ sudo apt install virtualbox virtualbox-ext-pack

https://linuxhint.com/install-virtualbox-linux-mint/

Onedrive replacement (nextcloud)

https://blog.containerize.com/2021/06/18/how-to-install-nextcloud-with-apache-on-ubuntu-server/

You can access microsoft products at portal.office.com

Selecting a distribution

[https://distrochooser.de/en">https://distrochooser.de/en](https://distrochooser.de/en%22%3ehttps:/distrochooser.de/en)

Create a boot disk

https://linuxmint-installation-guide.readthedocs.io/en/latest/burn.html

Download Iso image: https://www.linuxmint.com/download.php

Download rufus: https://rufus.ie/en/#google_vignette

Find a usb drive: 8 gigs should be enough

Instructions: [https://linuxhint.com/installing\_linux\_mint\_20\_from_usb/](https://linuxhint.com/installing_linux_mint_20_from_usb/)

getting drivers for your current network card

Moving from Chrome to firefox

Export tabs

Extensions

Thunderbird

Ditching OneNote

Or using one note in linux

Unblock snapd https://itsfoss.com/enable-snap-support-linux-mint/

Install: https://linuxhint.com/install-microsoft-onenote-linux/

Joplin: https://joplinapp.org/help/#desktop-applications

wget -O - [https://raw.githubusercontent.com/laurent22/joplin/dev/Joplin\_install\_and_update.sh](https://raw.githubusercontent.com/laurent22/joplin/dev/Joplin_install_and_update.sh) | bash

https://github.com/laurent22/joplin

Plugins: https://github.com/joplin/plugins/blob/master/README#plugins

## Three finger gestures:

https://github.com/bulletmark/libinput-gestures

Dark mode everything

## Creating a Windows VM

Get your windows key

Powershell:

wmic path softwareLicensingService get OA3xOriginalProductKey

7GNQ6-JJBGF-VCRY4-VC6W7-PWGF8

Iso image: https://www.microsoft.com/en-us/software-download/windows10ISO

Poll for community favorite software:

https://www.linuxquestions.org/questions/2018-linuxquestions-org-members-choice-awards-128/

OneDrive: https://linuxhint.com/install-and-use-onedrive-on-linux-mint/

## Fingerprint scanner

$ sudo apt install libpam-fprintd

$ sudo pam-auth-update

Hit space to select fingerprint authorization then press enter

$ fprintd-enroll

Lift and place your finger several times

sing device /net/reactivated/Fprint/Device/0 
Enrolling right-index-finger finger. 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
Enroll 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
result: 
en roll-stage- passed 
en roll-stage- passed 
enroll- remove-and- retry 
en roll-stage- passed 
enroll- remove-and- retry 
en roll-stage- passed 
en roll-stage- passed 
en roll-stage- passed 
enroll-stage-passed 
enroll- retry-scan 
enroll- remove-and- retry 
en roll-stage- passed 
enroll-retry-scan 
enroll-stage-passed 
enroll-stage-passed 
enroll- retry-scan 
en roll-stage- passed 
enroll-stage-passed 
en roll -completed " class="jop-noMdConv">

Install Putty

# Screenshots (greenshot replacement)

### Install shutter

sudo add-apt-repository -y ppa:linuxuprising/shutter
sudo apt-get install -y shutter

### Fix for x11 error

I found a solution. In this file sudo nano /etc/gdm3/custom.conf uncomment this line WaylandEnable=false save and exit. Then run this command in the terminal sudo systemctl restart gdm3 Happy Ubuntu :)

### In Ubuntu add a custom shortcut for shutter

sh –c "shutter –s"

## Onedrive

```
sudo dnf install onedrive
```

```
onedrive

```

```
`onedrive --synchronize --verbose --dry-run`

```

```
onedrive --synchronize
```

systemctl --user enable onedrive
systemctl --user start onedrive
systemctl status --user onedrive

### Install Obsidian using Flatpak

1.  In your terminal, run the following command to install Obsidian:
    
    ```
    flatpak install flathub.obsidian.Obsidian 
    ```
    
2.  Open Obsidian by running the following command:
    
    ```
    flatpak run.obsidian.Obsidian
    ```
