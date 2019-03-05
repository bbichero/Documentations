Errors
------

When trying to install a pacakge with pip:
```
pip error : ImportError: cannot import name IncompleteRead
```
You need to reinstall python-pip
```
sudo apt-get uninstall --purgge python-pip
sudo apt-get autoremove
```

Install pip with given command:
`sudo easy_install pip`
