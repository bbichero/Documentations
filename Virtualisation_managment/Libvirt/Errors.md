Erros
------

*For adding additionnal debug add LIBVIRT_DEBUG=1 to your command*
[Debug virtualisation problems](https://fedoraproject.org/wiki/How_to_debug_Virtualization_problems?rd=Virtualization_tips)

When starting a new VM if you see:
```
sudo virsh start test-debian
error: Failed to start domain test-debian
error: Storage pool not found: no storage pool with matching name 'default'
```

You must define a default pool (it must be define when installing `libvirt`)
```
virsh pool-define /dev/stdin <<EOF
<pool type='dir'>
  <name>default</name>
  <target>
    <path>/var/lib/libvirt/images</path>
  </target>
</pool>
EOF
```

And now start the created pool:
```
virsh pool-start default
```
virsh pool-autostart default

When starting VM with `virsh start ${VM_NAME}`:
```
internal error: process exited while connecting to monitor: 2019-03-17T13:45:55.762999Z qemu-system-x86_64: -enable-kvm: unsupported machine type
Use -machine help to list supported machines
```
This happen because the attribute `machine` in XML definition of VM is invalid   
`pc` is the  most generic value and you must use it.
