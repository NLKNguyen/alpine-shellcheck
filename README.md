Alpine-ShellCheck
=================
Alpine Linux with [ShellCheck](https://github.com/koalaman/shellcheck) -- a static analysis tool for shell scripts

Minimalist image size: **22 MB** (download size is only 6 MB)

Include:

- Alpine Linux (5 MB)
- Shellcheck binary (16 MB)
- Object dependencies (1 MB)

[![Build Status](https://travis-ci.org/NLKNguyen/alpine-shellcheck.svg?branch=master)](https://travis-ci.org/NLKNguyen/alpine-shellcheck)

Image builds by Travis CI are automatically pushed to Docker Hub repository: [nlknguyen/alpine-shellcheck](https://hub.docker.com/r/nlknguyen/alpine-shellcheck/)

See the Docker Hub repository for more information.

# Maintainer Notes

2 Dockerfiles

- `builder/Dockerfile` is used to build shellcheck from source, which cloned from shellscheck GitHub repository, and collect output executable shellcheck binary and dependencies for easy retrieval. When it runs, the binaries will be copied out to the mounted directory.

- `./Dockerfile` is used to build the image that is based on `alpine:latest` and contains only the neccessary binaries for shellcheck to run. It is intended for the image to be able to use as a `shellcheck` CLI program. `/mnt` is the designated mount point.

## Build steps

From project directory:
```sh
docker build -t builder builder/
```

Then run this. The container will copy the binary and dependencies out to `package` directory in host machine

```sh
docker run --rm -it -v $(pwd):/mnt builder
```

Once the `package` directory is available, build the final image:

```sh
docker build -t nlknguyen/alpine-shellcheck .
```

These are essentially the steps that Travis CI carry on before pushing the final image to Docker Hub.
