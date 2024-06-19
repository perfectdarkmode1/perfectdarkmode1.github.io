---
draft: true
title: chroot
---

## Notes

- Jail similar to a virtual machine. You can only access what is in the jail.
- Programs must be available within the jail (in /jail/bin)

To get a chroot shell, copy /bin and /lib to the chroot environment folder:
```
sudo mkdir /jail/bin
sudo mkdir /jail/lib
sudo mkdir lib64
sudo cp -r /bin/* /jail/bin
sudo cp -r /lib/* /jail/lib
sudo cp -r /lib64/* /jail/lib64
```

Enter chroot
`sudo chroot /jail`

