Tar
------

Extract tar archive in current directory:
```
tar xf ${ARCHIVE_PATH}
```

Extract tar archive and string 1 leading component from filename:
```
tar xf --strip-components=1 ${ARCHIVE_PATH}
```

Get remote archive and extract it to current directory:
```
curl ${REMOTE_URL_ARCHIVE} | tar -x
```
