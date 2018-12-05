# Dummy project to collect Gerrit plugins

This project contains several submodules, each of which is a Gerrit plugin.

## Update bazlets revision

To update the bazlets revision on all plugins:

```
git submodule foreach  ../update-bazlets.py -r 0cdf281f110834b71ae134afe0a7e3fe346f0078 -b stable-2.14 -v 2.14.15
git submodule foreach 'git push origin HEAD:refs/for/stable-2.14 || echo not pushed'
```

## Format code

```
git submodule foreach 'git ls-files | grep java$ | xargs google-java-format -i'
git submodule foreach 'git commit -a -m "Format all Java files with google-java-format" || echo nothing to commit'
git submodule foreach 'git push origin HEAD:refs/for/stable-2.14 || echo not pushed'
```

## Format build files

```
git submodule foreach 'git ls-files | grep "WORKSPACE\|BUILD\|\.bzl$" | xargs buildifier -mode=fix'
git submodule foreach 'git commit -a -m "Format all Bazel build files with buildifier" || echo nothing to commit'
git submodule foreach 'git push origin HEAD:refs/for/stable-2.14 || echo not pushed'
```

## Update submodules

```
git submodule foreach 'git checkout -t origin/stable-2.14 || echo execute only once or so'
git submodule foreach 'git checkout stable-2.14 || echo no stable-2.14 branch'
git submodule foreach 'git pull || echo dirty status?'
git commit -a -m "Update submodules based on each latest branch tip" || echo cannot add or commit
git push origin HEAD:stable-2.14 || echo not pushed
```

