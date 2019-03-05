Erros
------

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
