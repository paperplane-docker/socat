# `paperplanecc/socat` 官方 Docker 镜像 [![Build Status](https://drone.paperplane.cc/api/badges/p01/socat/status.svg)](https://drone.paperplane.cc/p01/socat)

## 简介

本镜像 [`paperplanecc/socat`](https://hub.docker.com/r/paperplanecc/socat) 提供了 Linux 的 [socat](https://linux.die.net/man/1/) 命令行工具；常见的用法是将 Docker 的 UNIX Sock 通讯通过 TCP 协议的方式对外暴露。

点此访问 [源码](https://git.paperplane.cc/p01/socat)；点此访问 [Github 源码](https://github.com/paperplane-docker/socat)。

## 私有版本

将 `paperplanecc` 用户名替换为 `docker.p01.cc` 即可使用私有库版本。点此访问 [私有库镜像](https://docker.p01.cc/#!/taglist/socat)（需登录）。

## 用法

拉取镜像：

```bash
docker pull paperplanecc/socat
```

使用举例：通过 TCP 转发 Docker 的 UNIX Sock 通讯；
启动配置如下：

```yaml
services:
  socat:
    image: paperplanecc/socat
    container_name: socat
    restart: always
    ports:
      - '2375:2375'
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
    command: TCP-LISTEN:2375,fork UNIX-CONNECT:/var/run/docker.sock
```

随后可以通过 `2375` 端口访问 Docker Engine API。
