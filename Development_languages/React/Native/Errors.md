Errors
------

When running android app with `npm run android` on a project, you got:
```
...
FAILURE: Build failed with an exception.

* What went wrong:
Could not create service of type ScriptPluginFactory using BuildScopeServices.createScriptPluginFactory().
> Could not create service of type PluginResolutionStrategyInternal using BuildScopeServices.createPluginResolutionStrategy().
...
```
It's a problem with the java version, if you are running the version 11, you must downgrade to 8, for this    
you must know your `$JAVA_HOME` version with:
```
readlink -f /usr/bin/java | sed "s:bin/java::"
```

Replace the path of version 11 with the 8 version and export the var `$JAVA_HOME`.

After fix this error, if you got another error:
```
...
FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':unimodules-core:compileDebugJavaWithJavac'.
> Could not find tools.jar. Please check that /usr/lib/jvm/java-8-openjdk-amd64 contains a valid JDK installation.
...
```

Install  java 8 again:
```
sudo apt install openjdk-8-jdk
```
