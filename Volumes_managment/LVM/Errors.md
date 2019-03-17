Errors
------

After creating a pool you need to build it   
When executing build command: `virsh pool-build ${POOL_NAME}`
```
error: Failed to build pool ${POOL_NAME}
error: Storage pool already built: Format of device '/dev/${DISK_NAME}' does not match the expected format 'LVM2_member', forced overwrite is necessary
```

You need to build your pool with `--overwrite` option:   
`virsh pool-build --overwrite ${POOL_NAME}`
