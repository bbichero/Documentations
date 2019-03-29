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

#### Commit
You need to add `--signoff` to your commit
This will add a line with a sign mark (your name and email)   
Every commit must have a subject and a description
Do not execute your commit with the `-m` option   

#### Patch
For creating a path from your's commit:   
`git format-patch -${NUMBER_OF_NEW_LOCAL_COMMIT} HEAD`   
A patch file will be generated in the current directory

Always check your patch integrity with the kernel script `checkpatch.pl`   
`/usr/src/$(uname -r)/scripts/checkpatch.pl ${KERNEL_PATH}/${PATCH_NAME_FILE}`
