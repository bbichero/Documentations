Fork
------

Create a new repository in you personal account an pull it:
```
git pull git@${REMOTE_GIT_FQDN}:${REMOTE_USERNAME}/${REMOTE_PATH}.git
cd ${REMOTE_PATH}
```

Add original repository to upstream in local git configuration:
```
git remote add upstream git@${ORIGINAL_GIT_FQDN}:${ORIGINAL}/${ORIGINAL_REMOTE_PATH}
```

Pull repository data from original remote git repository:
```
git pull upstream master
```

Push all pulled data to newly created repository:
```
git push origin master
```

### Sync forked repository

fetch new changes:
```
git fetch upstream
```

Make sure you are on `master` branch:
```
git checkout master
```

Rewrite master branch with upstream commit:
```
git rebase upstream/master
```
