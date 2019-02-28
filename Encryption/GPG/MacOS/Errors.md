Errors
------

When try to git commit but this message appear:
```
error: gpg failed to sign the data
fatal: failed to write commit object
```

You must to relink brew package
```
brew upgrade gnupg
brew link --overwrite gnupg
brew install pinentry-mac
echo "pinentry-program /usr/local/bin/pinentry-mac" >> ~/.gnupg/gpg-agent.conf
killall gpg-agent
```

Test that everything work:
`echo "test" | gpg --clearsign`
