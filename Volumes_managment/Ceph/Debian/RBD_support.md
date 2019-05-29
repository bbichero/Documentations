RBD KVM support
------

Qemu (kvm) need to have rbd support to create / handle rbd files.
You need to clone, compile then install qemu manualy

Get qemu source:
```
git clone git://git.qemu.org/qemu.git
cd qemu
```

Install build dependencies:
```
sudo apt build-dep qemu-kvm
```

Configure it:
```
./configure --enable-rbd
```

Compile and install it:
```
make -j ${NUMBER_OF_VCPU_AVAILABLE}
sudo make install
```
