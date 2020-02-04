---
layout: post
title: 'Docker - Mac research log'
date: 2015-05-15
comments: true
categories: [docker]
---
## Docker - Mac research log

~~[Install by Mac](http://docs.docker.com/installation/mac/)~~

### Register Docker Hub

[Docker Hub](https://hub.docker.com/)

### Use Kitematic

[kitematic](https://kitematic.com/)

### Install Ubuntu

Search ubuntu on docker hub

![螢幕快照_2015-05-27_上午12_36_02.png](http://user-image.logdown.io/user/3170/blog/3202/post/276146/Ff44CHSxS5qn7co6RsdJ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-05-27_%E4%B8%8A%E5%8D%8812_36_02.png)

Run command

![螢幕快照_2015-05-27_上午12_36_51.png](http://user-image.logdown.io/user/3170/blog/3202/post/276146/qDNHEI6YQcS9QbfQsbio_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7_2015-05-27_%E4%B8%8A%E5%8D%8812_36_51.png)

```shell
docker pull ubuntu
```

#### Use `docker images`

```shell
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
ubuntu              latest              07f8e8c5e660        3 weeks ago         188.3 MB
```

#### build dockerfile

```shell
docker build . -t ubuntu_dev:16.04 -f local.Dockerfile
```

#### run container

`docker run -t -i ubuntu /bin/bash`

```shell
docker run -t -i ubuntu /bin/bash
root@b0cdeb409841:/#
```

#### docker run

```shell
docker run -idt --name <container name> -v <mount absolute path or ~ path>:<docker path> <IMAGE>:<TAG>
```

#### end container

```shell
exit
```

#### show container

`docker ps -a`

#### show running container

`docker ps`

#### show images

`docker images`

#### enter docker container

`docker exec -it <container id> bash`

#### show log

`docker logs <container id>`
