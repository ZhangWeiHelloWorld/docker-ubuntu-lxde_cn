# docker-ubuntu-lxde VNC

[![Docker Pulls](https://img.shields.io/docker/pulls/dazhangwei/docker-ubuntu-lxde_cn?style=for-the-badge)](https://hub.docker.com/r/dazhangwei/docker-ubuntu-lxde_cn)

[基于 yama07/docker-ubuntu-lxde 修改](https://github.com/yama07/docker-ubuntu-lxde)

## 项目介绍

这是一个基于 Docker 的 Ubuntu LXDE/LXQt 桌面环境，支持通过 VNC(x11vnc, noVNC) 进行远程桌面连接。

内置中文环境（支持 ibus-pinyin 输入法），即使使用 `-u` 参数以普通用户身份启动，仍可使用 `sudo` 命令。

![屏幕截图](https://raw.githubusercontent.com/ZhangWeiHelloWorld/docker-ubuntu-lxde_cn/master/screenshot/ubuntu-22.04_arm.png)
![屏幕截图](https://raw.githubusercontent.com/ZhangWeiHelloWorld/docker-ubuntu-lxde_cn/master/screenshot/ubuntu-24.04_arm.png)

## 支持标签

- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/dazhangwei/docker-ubuntu-lxde_cn/24.04-vnc_cn?style=flat-square)](https://hub.docker.com/r/dazhangwei/docker-ubuntu-lxde_cn/tags?name=24.04-vnc_cn)
  `24.04-vnc_cn`, `latest-vnc`: 基于 Ubuntu24.04 的 LXQt 桌面 [(vnc/Dockerfile.ubuntu24.04)](https://github.com/ZhangWeiHelloWorld/docker-ubuntu-lxde_cn/blob/master/vnc/Dockerfile.ubuntu24.04)

- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/dazhangwei/docker-ubuntu-lxde_cn/22.04-vnc_cn?style=flat-square)](https://hub.docker.com/r/dazhangwei/docker-ubuntu-lxde_cn/tags?name=22.04-vnc_cn)
  `22.04-vnc_cn`: 基于 Ubuntu24.04 的 LXQt 桌面 [(vnc/Dockerfile.ubuntu22.04)](https://github.com/ZhangWeiHelloWorld/docker-ubuntu-lxde_cn/blob/master/vnc/Dockerfile.ubuntu22.04)
- [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/dazhangwei/docker-ubuntu-lxde_cn/20.04-vnc_cn?style=flat-square)](https://hub.docker.com/r/dazhangwei/docker-ubuntu-lxde_cn/tags?name=20.04-vnc_cn)
  `20.04-vnc_cn`: 基于 Ubuntu24.04 的 LXQt 桌面 [(vnc/Dockerfile.ubuntu20.04)](https://github.com/ZhangWeiHelloWorld/docker-ubuntu-lxde_cn/blob/master/vnc/Dockerfile.ubuntu20.04)

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

```bash
docker run -p 6080:80 \
  -p 5900:5900 \
  -itd \
  --privileged \
  -e PASSWD=ruaho1234 \
  -v /home/ubuntu/:/home/xxxx/ \
  --name docker-ubuntu-lxde_cn  4893b4cd8446
```

容器内的桌面环境设置默认保存在用户目录，建议通过 `-v ${HOME}/container_home:/home/xxxx` 挂载目录以持久化配置（注意：**必须提前创建**挂载目录避免权限错误）

### 客户端连接

#### noVNC

通过浏览器访问：
http://<Docker 主机 IP>:<novnc_port>/vnc.html
密码：设置的 loginPasswd

## 构建镜像

Docker 镜像的构建方法如下（请根据需要修改镜像名称和标签）：

```bash
$ git clone https://github.com/ZhangWeiHelloWorld/docker-ubuntu-lxde_cn.git
$ docker build \
    -t lxde_vnc:ubuntu24.04 \
    -f ./vnc/Dockerfile.ubuntu24.04 \
    ./vnc
```
