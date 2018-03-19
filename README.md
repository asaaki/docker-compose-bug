# docker-compose bug

```sh
$ docker-compose build bug
Building bug
ERROR: Error processing tar file(exit status 1): open /bug/linkdir/realfile: no such file or directory
```

versus

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