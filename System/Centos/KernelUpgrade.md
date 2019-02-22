Kernel upgrade
------

[Tutorial link](https://www.tecmint.com/install-upgrade-kernel-version-in-centos-7/)

Install EL repos
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```

List availale kernel release
`yum --disablerepo="*" --enablerepo="elrepo-kernel" list available`

Install latest stable kernel version
`yum --enablerepo=elrepo-kernel install kernel-ml`

Then you must to reboot you machine to make the change permanent
`reboot`

### Set default kernel version at boot
Edit grub file
`sudo vi /etc/default/grub`

Set `GRUB_DEFAULT=0`
This will select the first version available at boot

Now you need to recreate kernel configuration
`grub-mkconfig -o /boot/grub2/grub.cfg`
