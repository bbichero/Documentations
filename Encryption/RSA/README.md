RSA commands
------

Generate a RSA couple of private / public keys:
```
ssh-keygen -f ${KEYS_PATH} -b ${BIT_LENGTH}
```
Enter a pathphrase (or not) and the generation end.

Generate a ed25519 couple of private / public keys:
```
ssh-keygen -t ed25519 -a 100 -f ${KEYS_PATH}
```
`-a` option is used for amount of rounds
