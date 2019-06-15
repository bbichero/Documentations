Encrypted LVM with Luks
------

[Hetzner RAID encrypted LVM debian](https://www.sysorchestra.com/hetzner-root-server-with-dual-hardware-raid-1-and-lvm-on-luks-on-debian-9/)

Start your server update apt repo and install required packages:
```
sudo apt update
sudo apt install busybox dropbear dropbear-initramfs
```

Reboot your server in rescue mode,    
Save your new system:
```
mkdir /rootbackup
mount /dev/vg0/root /mnt
mount /dev/vg0/var /mnt/var
...

rsync -a /mnt/ /rootbackup/
```

Umount all mounted disk and disable LVM2:
```
umount /mnt/var
umount /mnt

vgchange -a n vg0
```

Restart LVM2
```
sudo systemctl restart lvm2
sudo systemctl restart lvm2-lvmetad.socket

vgchange -a n vg0
```

Remove LVM volume and recreate a new for Luks device:
```
parted /dev/sda
print free # check which partition contains the LVM. Mind the "Start" value of that partition which should be 538MB
rm 2 # Remove the partition
mkpart primary 538MB -1s # Change the "Start" value of sda2 if it differs
quit
```

Create Luks dev
```
cryptsetup --cipher aes-xts-plain64 --key-size 512 --hash sha256 --iter-time 6000 luksFormat /dev/sda2
```
