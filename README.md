## ubunto IMG 받아서 nginx 설치, Dockerfile 생성

1. rm, rmi
```
$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
$ sudo docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

2. pull, run
```
$ sudo docker pull ubuntu:22.04
$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       22.04     fd1d8f58e8ae   2 weeks ago   77.9MB

$ sudo docker run -itd --name ubuntu-nginx ubuntu:22.04
$ sudo docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS         PORTS     NAMES
844cb6901cb9   ubuntu:22.04   "/bin/bash"   32 seconds ago   Up 4 seconds             ubuntu-nginx
```

3. install nginx
```
$ sudo docker exec -it ubuntu-nginx bash
$ apt-get update
$ apt-get install nginx
```

4. Dockerfile 생성
```
$ cat Dokcerfile
FROM ubuntu:22.04
RUN apt-get update
RUN apt-get install -y nginx
EXPOSE 80
CMD ["nginx" ,"-g", "demon off";]

$ sudo docker build -t test .
[+] Building 8.2s (7/7) FINISHED                                           docker:default
 => [internal] load build definition from Dockerfile                                 0.0s
 => => transferring dockerfile: 147B                                                 0.0s
 => [internal] load metadata for docker.io/library/ubuntu:22.04                      0.0s
 => [internal] load .dockerignore                                                    0.0s
 => => transferring context: 2B                                                      0.0s
 => [1/3] FROM docker.io/library/ubuntu:22.04                                        0.0s
 => CACHED [2/3] RUN apt-get update                                                  0.0s
 => [3/3] RUN apt-get install -y nginx                                               8.1s
 => exporting to image                                                               0.2s
 => => exporting layers                                                              0.1s
 => => writing image sha256:50273b2ec7cf128f853123a3e86ca914a2d3268eeed8eefa9dfd679  0.0s
 => => naming to docker.io/library/test                                              0.0s

$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
test         latest    50273b2ec7cf   4 seconds ago   182MB
```
