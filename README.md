# verification-drone-exec-and-circleci-local-execute

verification code of `drone exec` and `circleci local execute`.

## Summary

`drone exec` command may change host files, but `circleci local execute` doesn't change them.

## drone and circleci version

* drone 1.1.0
* circleci 0.1.1973+68f6a97

## Details

`drone exec` command may change host files.

```
$ ls
README.md

$ drone --version
drone version 1.1.0

$ drone exec
[create file:0] + echo foo > foo.txt

$ ls
README.md  foo.txt
```

On the other hand, `circleci local execute` command doesn't change host files.

```
$ circleci version
0.1.1973+68f6a97

$ circleci local execute
Docker image digest: sha256:525c91e01875050fbf65cdb4bc83a45744c54f9027fa05f76f88713f3d37f4e3
Unable to find image 'circleci/picard@sha256:525c91e01875050fbf65cdb4bc83a45744c54f9027fa05f76f88713f3d37f4e3' locally
sha256:525c91e01875050fbf65cdb4bc83a45744c54f9027fa05f76f88713f3d37f4e3: Pulling from circleci/picard
4064ffdc82fe: Pull complete
1d24d837342c: Pull complete
f6ac02792af3: Pull complete
7fb52b073c33: Pull complete
38e4386c4de7: Pull complete
3d918f9110dc: Pull complete
Digest: sha256:525c91e01875050fbf65cdb4bc83a45744c54f9027fa05f76f88713f3d37f4e3
Status: Downloaded newer image for circleci/picard@sha256:525c91e01875050fbf65cdb4bc83a45744c54f9027fa05f76f88713f3d37f4e3
====>> Spin up Environment
Build-agent version 0.0.7725-9681bc36 (2018-08-09T15:10:50+0000)
Starting container busybox
  using image busybox@sha256:954e1f01e80ce09d0887ff6ea10b13a812cb01932a0781d6b0cc23f743a874fd

Using build environment variables:
  BASH_ENV=/tmp/.bash_env-localbuild-1556411928
  CI=true
  CIRCLECI=true
  CIRCLE_BRANCH=
  CIRCLE_BUILD_NUM=
  CIRCLE_JOB=build
  CIRCLE_NODE_INDEX=0
  CIRCLE_NODE_TOTAL=1
  CIRCLE_REPOSITORY_URL=
  CIRCLE_SHA1=
  CIRCLE_SHELL_ENV=/tmp/.bash_env-localbuild-1556411928
  CIRCLE_WORKING_DIRECTORY=~/project

====>> echo foo > foo.txt
  #!/bin/sh -eo pipefail
echo foo > foo.txt
Success!

$ ls
README.md
```

## Reference

* drone exec
  * https://docs.drone.io/cli/install/
  * https://docs.drone.io/cli/drone-exec/
* circleci local execute
  * https://circleci.com/docs/2.0/local-cli/
