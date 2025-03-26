# docker-ubuntu-lxde VNC

[![Docker Pulls](https://img.shields.io/docker/pulls/yama07/docker-ubuntu-lxde?style=for-the-badge)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde)
[![GitHub](https://img.shields.io/github/license/yama07/docker-ubuntu-lxde?style=for-the-badge)](https://github.com/yama07/docker-ubuntu-lxde)

## 项目介绍

这是一个基于 Docker 的 Ubuntu LXDE/LXQt 桌面环境，支持通过 VNC(x11vnc, noVNC) 进行远程桌面连接。

内置日语环境（支持 ibus-mozc 输入法），即使使用 `-u` 参数以普通用户身份启动，仍可使用 `sudo` 命令。

![屏幕截图](https://raw.githubusercontent.com/yama07/docker-ubuntu-lxde/master/screenshot/VNC-ubuntu24.04_ja.png)
![屏幕截图](https://raw.githubusercontent.com/yama07/docker-ubuntu-lxde/master/screenshot/noVNC-ubuntu24.04_ja.png)

## 支持标签

- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yama07/docker-ubuntu-lxde/24.04-vnc_ja?style=flat-square)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde/tags?name=24.04-vnc_ja)
  `24.04-vnc_ja`, `noble-vnc_ja`, `latest-vnc`: 基于 Ubuntu24.04 的 LXQt 桌面 [(vnc/Dockerfile.ubuntu24.04)](https://github.com/yama07/docker-ubuntu-lxde/blob/master/vnc/Dockerfile.ubuntu24.04)
  
- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yama07/docker-ubuntu-lxde/24.04-vnc-slim_ja?style=flat-square)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde/tags?name=24.04-vnc-slim_ja)
  `24.04-vnc-slim_ja`, `noble-vnc-slim_ja`: Ubuntu24.04 精简版 LXQt [(vnc/Dockerfile.ubuntu24.04_slim)](https://github.com/yama07/docker-ubuntu-lxde/blob/master/vnc/Dockerfile.ubuntu24.04)
- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yama07/docker-ubuntu-lxde/22.04-vnc_ja?style=flat-square)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde/tags?name=22.04-vnc_ja)
  `22.04-vnc_ja`, `jammy-vnc_ja`: 基于 Ubuntu22.04 [(vnc/Dockerfile.ubuntu22.04)](https://github.com/yama07/docker-ubuntu-lxde/blob/master/vnc/Dockerfile.ubuntu22.04)
- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yama07/docker-ubuntu-lxde/22.04-vnc-slim_ja?style=flat-square)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde/tags?name=22.04-vnc-slim_ja)
  `22.04-vnc-slim_ja`, `jammy-vnc-slim_ja`: Ubuntu22.04 精简版 [(vnc/Dockerfile.ubuntu22.04_slim)](https://github.com/yama07/docker-ubuntu-lxde/blob/master/vnc/Dockerfile.ubuntu22.04)
- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yama07/docker-ubuntu-lxde/20.04-vnc_ja?style=flat-square)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde/tags?name=20.04-vnc_ja)
  `20.04-vnc_ja`, `focal-vnc_ja`: 基于 Ubuntu20.04 [(vnc/Dockerfile.ubuntu20.04)](https://github.com/yama07/docker-ubuntu-lxde/blob/master/vnc/Dockerfile.ubuntu20.04)
- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/yama07/docker-ubuntu-lxde/20.04-vnc-slim_ja?style=flat-square)](https://hub.docker.com/r/yama07/docker-ubuntu-lxde/tags?name=20.04-vnc-slim_ja)
  `20.04-vnc-slim_ja`, `focal-vnc-slim_ja`: Ubuntu20.04 精简版 [(vnc/Dockerfile.ubuntu20.04_slim)](https://github.com/yama07/docker-ubuntu-lxde/blob/master/vnc/Dockerfile.ubuntu20.04)

## 使用指南

### 启动 Docker 容器

参数选项如下：

- `-p vnc_port:5900`
  设置 VNC 客户端连接端口。如果仅使用 noVNC 则无需设置
- `-p novnc_port:80`
  设置 Web 浏览器连接端口。如果不使用 noVNC 则无需设置
- `-u user:group`
  设置容器启动的 UID/GID（默认使用 root 用户）
- `-e USER=loginUser`
  设置登录用户名（默认 developer，root 用户启动时为 root）
- `-e PASSWD=loginPasswd`
  设置登录密码（默认 vncpasswd）
- `-e RESOLUTION=WxHxD`
  设置屏幕分辨率（默认 1280x720x24）

如果连接后无法显示登录界面，尝试添加 `--privileged` 参数

容器内的桌面环境设置默认保存在用户目录，建议通过 `-v ${HOME}/container_home:/home/yama07` 挂载目录以持久化配置（注意：**必须提前创建**挂载目录避免权限错误）

### 客户端连接

#### VNC 客户端
启动后使用 RealVNC 或 UltraVNC 客户端连接：
地址：<Docker 主机 IP>:<vnc_port>
密码：设置的 loginPasswd

#### noVNC
通过浏览器访问：
http://<Docker 主机 IP>:<novnc_port>/vnc.html
密码：设置的 loginPasswd

## 构建镜像
Docker 镜像的构建方法如下（请根据需要修改镜像名称和标签）：

```bash
$ git clone https://github.com/yama07/docker-ubuntu-lxde.git
$ docker build \
    -t lxde_vnc:ubuntu24.04_ja \
    -f ./vnc/Dockerfile.ubuntu24.04 \
    ./vnc
```
