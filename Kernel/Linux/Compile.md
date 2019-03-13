Compile Linux Kernel
------

Environment
```
KERNEL_VERSION: 5.0.1
```

Download linux kernel source from official git:
`git clone https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/`

You need to install NCURSES lib to launch menuconfig
`sudo apt-get install libncurses-dev`

Enter in directory and launch menuconfig
```
cd linux
make menuconfig
```
Choose some usefull modules, then save `.config` file (in current dir)

Following vCPU you have you may perform kernel compilling with more than 1 vCPU
`make -j ${CPU_NB_AVAILABLE}`

Install modules
`sudo make modules_install`

Copy bzImage, System.map and config created
```
sudo cp -iv arch/x86/boot/bzImage /boot/vmlinuz-${KERNEL_VERSION}
sudo cp -iv System.map /boot/System.map-${KERNEL_VERSION}
sudo cp -iv .config /boot/config-${KERNEL_VERSION}
```

Install kernel documentation
```
sudo install -d /usr/share/doc/linux-${KERNEL_VERSION}
sudo cp -r Documentation/* /usr/share/doc/linux-${KERNEL_VERSION}
```
