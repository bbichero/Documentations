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
`apt-get install bison gawk patch texinfo g++`

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
