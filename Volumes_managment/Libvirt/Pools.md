Pools
------

[Officiel Tuto](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/storage_pools#storage_pool_params_disk-based)


### Create pool based directory
Create a file `pool.xml`:
```
<pool type='dir'>
  <name>${POOL_NAME}</name>
    <target>
		<path>/${POOL_PATH}/${POOL_NAME}/</path>
	</target>
</pool>
```

Define pool:
`virsh pool-define pool.xml`

build, active and autoactive pool
```
virsh pool-build ${POOL_NAME}
virsh pool-start ${POOL_NAME}
virsh pool-autostart ${POOL_NAME}
```
