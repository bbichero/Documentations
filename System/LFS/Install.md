Install
------

Environment:
```
Distribution: Debian Stretch 8.9
Kernel version: Linux 4.9.0-8-amd64
```

Tutorial is available [here](https://www.lfscript.org/)

#### Match the prerequired

I. Disks:
- host disk with no prerequired
- LFS disk with at minimum 3 partitions
	1. /boot  [BIOS boot] -> 100Mo
	2. / [ext4] -> 10Go
	3. /home [ext4] -> 10Go
	4. /usr/src [ext4] -> 10Go
	5. swap [ext4] -> 1Go

II. RAM:
Host must have 2Go of RAM and 2Go of swap (1Go of each is enought but 2Go is recommended)

III. CPU:
2vCPU is recommended for the host

IV. Packages:
`ln -svf bash /bin/sh`
`apt-get install bison gawk patch texinfo g++ build-essential`

#### Partitions
Format each standar partitions (`root`, `home`, `usr/src`):   
`sudo mkfs.ext4 /dev/${PARTITION_PATH}`

For the swap parition:   
`mkswap /dev/${SWAP_PARTITION_PATH}`

Now create mounting point:
```
mkdir /mnt/install_root
mount -t ext4 /dev/${ROOT_PARTITION_PATH}

mkdir /mnt/install_root/home
mkdir /mnt/install_root/usr
mkdir /mnt/install_root/usr/src
mount -t ext4 /dev/${HOME_PARTITION_PATH}
mount -t ext4 /dev/${USR_SRC_PARTITION_PATH}
```

#### LFSscript

Once host's disk are configured get source code of LFSscript:   
`wget lfscript.org/latest.tar.xz`

Untar it:
```
tar xf lfscript${LFS_VERSION}
cd lifscript*
```

Execute LFSscript:    
`sudo ./lfscript -B -i /mnt/install_root`

You must create `/etc/fstab` file for partitions mounting at boot:
```
cat > /mnt/install_root/etc/fstab << "EOF"
# Begin /etc/fstab

# file system  mount-point  type     options             dump  fsck
#                                                              order
/dev/${ROOT_PARTITION_PATH}	/	ext4	defaults	1	1
/dev/${USR_SRC_PARTITION_PATH}	/usr/src	ext4	defaults	1	1
/dev/${HOME_PARTITION_PATH}	/home	ext4	defaults	1	1
/dev/${SWAP_PARTITION_PATH}	swap	swap	pri=1	0	0

proc           /proc        proc     nosuid,noexec,nodev 0     0
sysfs          /sys         sysfs    nosuid,noexec,nodev 0     0
devpts         /dev/pts     devpts   gid=4,mode=620      0     0
tmpfs          /run         tmpfs    defaults            0     0
devtmpfs       /dev         devtmpfs mode=0755,nosuid    0     0

# End /etc/fstab
EOF
```

You must create `/mnt/install_root/boot/grub/grub.cfg`
```
cat > /mnt/install_root/etc/fstab << "EOF"
# Begin /boot/grub/grub.cfg
set default=0
set timeout=5

insmod ext2
insmod part_gpt
set root='hd0,gpt2'

# Generic initramfs and root fs on LVM partition
menuentry "LFS Dev (LFS-7.0-Feb18) initrd lvm, Linux 3.0.4"
{
	linux  /vmlinuz-4.10.13-lfs-SVN-20170428 root=/dev/${ROOT_PARTITION_PATH} ro
	initrd /4.9.0-8-amd64
}
EOF
```

Create a rescue parition:
```
cd /tmp 
grub-mkrescue --output=grub-img.iso 
xorriso -as cdrecord -v dev=/mnt/intall_root/dev/cdrw blank=as_needed grub-img.iso
```

Install grub root disk:   
`sudo grub-install /dev/${LFS_DISK_PATH}`
