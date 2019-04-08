Export / Import
------

List gpg keys:
```
gpg --list-keys
```

Copy the key fingerprint to export specific key:
```
gpg --output mygpgkey_pub.gpg --armor --export ${KEY_FINGERPRINT}
gpg --output mygpgkey_sec.gpg --armor --export-secret-key ${KEY_FINGERPRINT}
```

Then export to remote server:
```
scp mygpgkey_pub.gpg mygpgkey_sec.gpg ${REMOTE_USER}@${REMOTE_IPV4}:~/
```

After connecting to remote server, import key:
```
gpg --import ~/mygpgkey_pub.gpg
gpg --allow-secret-key-import --import ~/mygpgkey_sec.gpg
```

List server keys and check if imported keys are presents:
```
gpg --list-keys
```

Remove previous exported key file on server and source host:
```
rm ~/mygpgkey_sec.gpg ~/mygpgkey_pub.gpg
```
