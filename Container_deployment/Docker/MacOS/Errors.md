Errors
------

When running `docker ps` command, got error:
```
docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
```

After a brew install, you must execute:
(Install macOS applications distributed as binaries)
```
brew cask install docker
```
