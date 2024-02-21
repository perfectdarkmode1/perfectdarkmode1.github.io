# Setting up RHEL8 VM1

download the disk iso on Redhat's website

Name RHEL8-VM1

accept defaults

set drive to 10 gigs

press "space" to halt autoboot

Select install

select language

configure timezone under time & date

go into installation destination and click "done"

### Network and hostname settings

1. change the hostname to server1.example.com

2. go to IPv4 settings in network and host and set to manual address: 192.168.0.110 netmask 24 gateway 192.168.0.1 then save

3. slide the on/off switch in the main menu to on

# Set Custom base URL to [https://cdn.redhat.com](https://cdn.redhat.com "https://cdn.redhat.com") in addition to setting Custom server URL to subscription.rhsm.redhat.com . It looks like if these options aren't ticked the values get set to the blank string rather than a sensible default.

### Set root password

### Change the boot order

1. power off the vm

2. Set boot sequence to hard disk first then optical, remove floppy

![aff48dd4988b803575526ea399c96123.png](file:///C:/Users/tdave/.config/joplin-desktop/resources/eb5743e5bcc244fdbb4b8d61a50d805e.png)

Accept license terms and create user

?Enable geographical location?

ssh from host os with putty
