Contribute to Linux Kernel
------

Links:   
[Kernel contrib tuto](https://kernelnewbies.org/FirstKernelPatch)

```
Environment:
Kernel: 4.12.7
Distribution: LFS
```

### Environment
#### Editor
Vim:

turn syntax highlighting on, and show the file name in the terminal title bar.
Most distributions compile vim so that 8 space tabs are the default. If you find they're not the default, you will need to add the following line to your .vimrc:

```
filetype plugin indent on
set title
syntax on
set tabstop=8
set softtabstop=8
set shiftwidth=8
set noexpandtab
```
