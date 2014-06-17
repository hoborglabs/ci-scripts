# CI Scripts

All sorts of helper scripts for CI servers, that you don't want to keep in your project repository.

This scripts should complement existing Jenkins/Hudson plugins. If there is a plugin that does the same thing as
one of this scripts, don't hesitate and contact me at wojtek@hoborglabs.com




## Git



### add-and-commit

Adds, commits and push given folders or files.  
Useful when you generate distribution artefacts during build.

```BASH
$ ./git/add-and-commit -d "./dist ./CHANGELOG" -m "CI successful build"
  Looking for changes in: ./dist ./CHANGELOG
  Files to be commited:
     * ./dist/app.min.js
     * ./dist/app.jsm
     * ./CHANGELOG
  Commited and pushed: 7d8256a, "CI successful build"
```

Or if there are no changes
```BASH
$ ./git/add-and-commit -d "./dist ./CHANGELOG" -m "CI successful build"
  Looking for changes in: ./dist ./CHANGELOG
  No changes found.
```



### tag-next-version

Creates next tag based on given base version.

```BASH
$ ./git/tag-next-version -v v1.2 -c "CHANGELOG" -m "CI bugfix release"
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
$ ./git/tag-next-version -v v2.0 -c "CHANGELOG" -m "CI bugfix release"
  Current version: v1.2.12
  Tagged v2.0.0
  Saved changelog to: CHANGELOG
```
