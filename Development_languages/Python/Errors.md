Errors
------

### Workaround openmediavault python 3.5 weakref.py error   
curl -L https://raw.githubusercontent.com/python/cpython/3.5/Lib/weakref.py > /usr/lib/python3.5/weakref.py


### When executin python   
```
ImportError: no module named site
```

This error come from invalid python path, so unset python env vars
```
unset PYTHONPATH
unset PYTHONHOME
```
