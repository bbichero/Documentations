Errors
------

When installing `node-sass` with npm:   
```
Error: Node Sass does not yet support your current environment: Linux 64-bit with Unsupported runtime (67)
```
You need to install `g++` and rebuilt package:   
`npm rebuild node-sass`
