Errors
------

```
“RTNETLINK answers: File exists” when running ifup
```

You need to flush network device before `ifup` and `ifdown`   
```
sudo ip addr flush dev ${NET_INT}
```
