# docker-compose bug

## Fixed with docker-compose 1.20.1!

See: <https://github.com/docker/compose/releases/tag/1.20.1>

---

`docker-compose build` (and therefore `up --build`) fails if the project to be build has a symlinked folder in it. Somehow the resolution of it does not work properly anymore.

Tool: <https://github.com/docker/compose>

## `docker-compose.yml`

Version 2 and 3 are broken, so the config version seems not to matter:

```yml
version: '3'
services:
  bug:
    build: .
```

## Run and result

### Broken

```sh
$ docker-compose build bug
Building bug
ERROR: Error processing tar file(exit status 1): open /bug/linkdir/realfile: no such file or directory
```

versus

### Working

```sh
$ docker build -t docker-compose-bug .
Sending build context to Docker daemon  52.22kB
Step 1/2 : FROM busybox
 ---> f6e427c148a7
Step 2/2 : COPY bug /bug
 ---> 8e7e676e6d57
Successfully built 8e7e676e6d57
Successfully tagged docker-compose-bug:latest
```

## Affected versions

So far we could test it with …

- `1.19.0` on Arch Linux
- `1.20.0-rc2` on macos/Docker4Mac Edge

So this issue seems to be around for a while (at least since [2018-02-07](https://github.com/docker/compose/releases/tag/1.19.0)).