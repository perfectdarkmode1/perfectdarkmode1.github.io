
`dd if=/dev/zero of=./mydisk.img bs=1M count=1024 conv=fsync ` 
  `xxd mydisk.img | less  `
  `hexedit mydisk.img ` `
  `xxd mydisk.img | less  `
 ` hexedit mydisk.img  `
 ` xxd mydisk.img | less  `
  `ls -la mydisk.img  `
  `xxd mydisk.img | less  `
  `losetup --help  `
 ` sudo losetup -f ./mydisk.img  `
  `ll /dev/*l*  `
* `mount | grep l  `
  `lsblk  `
  `ll /dev/loop0 `
  `sudo fdisk /dev/loop0 print `
  `sudo fdisk /dev/loop0 `
  `sudo partprobe `
  `sudo fdisk /dev/loop0 `
  `sudo partprobe `
  `lsblk `
  `ll /dev/loop0* `
  `sudo losetup --help `
  `sudo losetup -d /dev/loop0 `
  `sudo losetup -f ./mydisk.img `
 `ll /dev/loop0* `
 ` sudo losetup -d /dev/loop0 `
  `sudo losetup -Pf ./mydisk.img `
 ` ll /dev/loop0* 10014  lsblk `
  `man tail `
 ` sudo mkfs.xfs /dev/loop0p1 `
  `sudo mkdir /mnt/loop `
  `sudo mount /dev/loop0p1 /mnt/loop `
 ` ll /mnt/loop `
  `df /mnt/loop `
  `echo 'test' > /mnt/loop/test.txt `
  `echo 'test' | sudo tee /mnt/loop/test.txt `
  `ll /mnt/loop `
 ` sudo cat /mnt/loop/test.txt `
  `grep test mydisk.img `
  `xxd mydisk.img | grep test `
 ` ll /dev/loop0* `
  `sudo mkdir /mnt/loop/test `
  `echo 'test' | sudo tee /mnt/loop/test/test2.txt `
 ` sync `
  `sudo tree /mnt/loop `
  `man pvcreate `
  `dd if=/dev/zero of=./mydisk2.img bs=1M count=1024 conv=fsync `
  `sudo losetup -Pf ./mydisk2.img `
  `ll /dev/loop* `
  `lsblk `
  `sudo pvcreate /dev/loop1 `
  `sudo pvdisplay `
 ` sudo vgcreate --help `
  `sudo vgcreate loop /dev/loop1 /dev/loop0p1 `
  `sudo vgdisplay `
 ` ll mydisk* `
  `sudo lvdisplay `
  `lsblk -o +FSTYPE `
  `sudo lvcreate -a y -L 100% -n loop-lv loop `
 ` sudo lvcreate -a y -l100% -n loop-lv loop `
  `sudo lvcreate -a y -l100%FREE -n loop-lv loop `
  `sudo partprobe `
  `lsblk -o +FSTYPE `
 ` sudo mkfs.xfs /dev/loop/loop-lv `
  `sudo mount /dev/loop/loop-lv /mnt/loop `
  `df -h /mnt/loop `
  `sudo lvdisplay `
 ` ll /dev/loop `
 ` ll /dev/dm-3`
  
other window included, somewhere in there,
   
 ` ls -la /dev/loop0*  `
 ` sudo umount /mnt/loop  `
  `lsblk `
  `sudo partprobe `
  `lsblk +o FSTYPE `
  `lsblk -o +FSTYPE `
  `sudo pvcreate /dev/loop0p1 `
  `sudo partprobe `
`lsblk -o +FSTYPE``

`dd` just gave me a file with zeroes, `losetup` just let me mount a file as a looback block device
 

everything else is relevant with literally any block device
  
inside of fdisk we used `o` to create an MBR, `w` to write it, `a` to add a partition, and then accepted defaults for size (as fdisk aligned to the block device with safe defaults, based on its block size), then `w` to write that partition data
