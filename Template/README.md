Package Name
------

### Environment:
General
```
# Distribution and kernel version
# For Distribution version:
# cat /etc/*-release
# or lsb_release -a
# And for kernel version :
# uname -a
# here an example:
Distribution: Debian buster/sid
Kernel: Linux 4.9.0-4-amd64
```

Packages
```
# Execute: package-name --version on your system
# example node --version
```

### Variables:
#### Global
Every variable you have in your documentations step must be here
When I say variable I mean command line part that need to be change following
system version, user distribution, kernel release and local environment (absolut path, size, name ...)

Example:

Local SSH version: (ex: `OpenSSH_7.9p1`) 
`SSH_VERSION`
