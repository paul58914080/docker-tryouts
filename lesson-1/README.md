## Creating a new image

```dockerfile
# Specify the base image
FROM alpine

# Download and install dependencies
RUN apk add --update redis
RUN apk add --update gcc

# Bootstrap\startup command
CMD ["redis-server"]
```

### `FROM alpine`

Take an existing base image from docker hub, in this case `alpine` into the cache

```
$ docker build -t paul58914080/redis-gcc:latest .

Sending build context to Docker daemon  4.096kB
Step 1/4 : FROM alpine
latest: Pulling from library/alpine
e6b0cf9c0882: Pull complete 
Digest: sha256:2171658620155679240babee0a7714f6509fae66898db422ad803b951257db78
Status: Downloaded newer image for alpine:latest
 ---> cc0abc535e36
```

### `RUN apk add --update redis`

Looks back at the previous step and create a temporary container from the base image of `alpine` with the following


| File system     | Startup command              |
|-----------------|------------------------------|
| **alpine**      | `RUN apk add --update redis` |

This will execute the command and install `redis` which would result in the following

> ##### Snapshot

| File System      | Startup Command                 |
|:----------------:|:-------------------------------:|
| **alpine**       |                                 |

After creating the image snapshot and it would delete the temporary container

```
Step 2/4 : RUN apk add --update redis
 ---> Running in f99021219b67
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/community/x86_64/APKINDEX.tar.gz
(1/1) Installing redis (5.0.7-r0)
Executing redis-5.0.7-r0.pre-install
Executing redis-5.0.7-r0.post-install
Executing busybox-1.31.1-r8.trigger
OK: 7 MiB in 15 packages
Removing intermediate container f99021219b67
 ---> e58652a066f9
```

### `RUN apk add --update gcc`

Creates a temporary container from the previous image (`alpine` + `redis`) and adds the startup command 

| File system               | Startup command            |
|---------------------------|----------------------------|
| **alpine**, **redis**     | `RUN apk add --update gcc` |


This will execute the command and install `gcc` which would result in the following

> ##### Snapshot

| File system                 | Startup command                 |
|:---------------------------:|:-------------------------------:|
| **alpine**, **redis**       |                                 |

After creating the image snapshot and it would delete the temporary container

```
Step 3/4 : RUN apk add --update gcc
 ---> Running in 0ce0f8320e39
(1/10) Installing libgcc (9.2.0-r3)
(2/10) Installing libstdc++ (9.2.0-r3)
(3/10) Installing binutils (2.33.1-r0)
(4/10) Installing gmp (6.1.2-r1)
(5/10) Installing isl (0.18-r0)
(6/10) Installing libgomp (9.2.0-r3)
(7/10) Installing libatomic (9.2.0-r3)
(8/10) Installing mpfr4 (4.0.2-r1)
(9/10) Installing mpc1 (1.1.0-r1)
(10/10) Installing gcc (9.2.0-r3)
Executing busybox-1.31.1-r8.trigger
OK: 102 MiB in 25 packages
Removing intermediate container 0ce0f8320e39
 ---> 57e38284a863
```

### `CMD ["redis-server"]`

Create a temporary container from the previous image (`alpine` + `redis` + `gcc`) and adds the start-up command 

| File system               | Startup command     |
|---------------------------|---------------------|
| **alpine**, **redis**     | `["redis-server"]` |


Remove the temporary container and create a new snapshot of this image which would result in 

> ##### Snapshot

| File system                    | Startup command                 |
|:------------------------------:|:-------------------------------:|
| **alpine**, **redis**, **gcc** | `["redis-server"]`              |

```
Step 4/4 : CMD ["redis-server"]
 ---> Running in 2cb2ce385390
Removing intermediate container 2cb2ce385390
 ---> 13ef59c99821
Successfully built 13ef59c99821
Successfully tagged paul58914080/redis-gcc:latest
```

