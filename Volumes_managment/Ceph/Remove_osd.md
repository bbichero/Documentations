Remove properly OSD
------

From [Sebastien Han blog](http://www.sebastien-han.fr/blog/2015/12/11/ceph-properly-remove-an-osd/)

Disconnect osd from cluster:
```
ceph osd out ${OSD_ID}
```

Stop Object Storage Daemon:
```
service ceph stop osd.${OSD_ID}
```

Remove osd from CRUSH map:
```
ceph osd crush remove osd.${OSD_ID}
```

Remove the OSD authentication key:
```
ceph auth del osd.${OSD_ID}
```

Remove OSD:
```
ceph osd rm ${OSD_ID}
```
