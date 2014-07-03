# CI Scripts

All sorts of helper scripts for CI servers, that you don't want to keep in your project repository.

This scripts should complement existing Jenkins/Hudson plugins. If there is a plugin that does the same thing as
one of this scripts, don't hesitate and contact me at wojtek@hoborglabs.com




## Git

Set of scripts for making CI easy with jenkins or hudson.




### add-and-commit

Adds, commits and push given folders or files.  
Useful when you generate distribution artefacts during build. This script will take care of the fact that you might not
be on a branch (hudson/jenkins checkouts revisions not branches)

```BASH
$ /opt/ci-scripts/git/add-and-commit -d "./dist ./CHANGELOG" -m "CI successful build"
  Looking for changes in: ./dist ./CHANGELOG
  Files to be commited:
     * ./dist/app.min.js
     * ./dist/app.jsm
     * ./CHANGELOG
  Commited and pushed: 7d8256a, "CI successful build"
```

Or if there are no changes
```BASH
$ /opt/ci-scripts/git/add-and-commit -d "./dist ./CHANGELOG" -m "CI successful build"
  Looking for changes in: ./dist ./CHANGELOG
  No changes found.
```

When you build on hudson or jenkins from a `release` branch
```BASH
$ /opt/ci-scripts/git/add-and-commit -b release -d "./dist" -m "CI successful build"
  Currently not on any branch
  local and origin HEADs looks the same (9e40786). Switching to branch 'release'
  Looking for changes in: ./dist
  No changes found.
```




### tag-next-version

Creates next tag based on given base version.

This script will take care of the fact that you might not be on a branch when for instance running build on hudson or
jenkins, just use `-b` to provide branch name.

```BASH
$ /opt/ci-scripts/git/tag-next-version -v v1.2 -c "CHANGELOG" -m "CI bugfix release"
  Current version: v1.2.11
  Tagged v1.2.12
  Saved changelog to: CHANGELOG
$ git tag -ln1
...
v1.2.12         CI bugfix release
```

When releasing new version (minor or major) script will assume that lates tag reachable from current branch is the
previous tag.

```BASH
$ /opt/ci-scripts/git/tag-next-version -v v2.0 -c "CHANGELOG" -m "CI bugfix release"
  Current version: v1.2.12
  Tagged v2.0.0
  Saved changelog to: CHANGELOG
```

When you build on hudson on jenkins on `release` branch

```BASH
$ /opt/ci-scripts/git/tag-next-version -b release -v v1.2 -c "CHANGELOG" -m "CI bugfix release"
  Currently not on any branch
  local and origin HEADs looks the same (9e40786). Switching to branch 'release'
  Current version: v1.2.12
  Tagged v1.2.13
  Saved changelog to: CHANGELOG
```
