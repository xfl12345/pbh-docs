---
sidebar_position: 1
---

# Docker

Docker 部署是 PeerBanHelper 推荐的部署方式。使用 PBH 提供的示例配置文件和 CLI 命令，PBH 将能够跟随系统自动启动，并在后台运行（除非手动停止）。

## 获取版本标签

首先访问 [PBH最新版版本发布页](https://github.com/PBH-BTN/PeerBanHelper/releases/latest)，向下滚动，找到如图所示的 “Docker 用户” 章节，并复制镜像标签备用。

![image-tag](./assets/docker-tag.png)

## 使用 Docker Compose 部署

找一个合适的位置创建一个目录作为 PBH 的数据存放位置，并将工作目录切换到此位置。
保存下面的内容到 docker-compose.yml 文件。

```yaml
version: "3.9"
services:
  peerbanhelper:
    image: ghostchu/peerbanhelper:latest
    # 若使用镜像源则不能使用 latest 标签，请使用具体版本号，否则可能会导致拉取到的镜像是远古版本
    # image: registry.cn-hangzhou.aliyuncs.com/ghostchu/peerbanhelper:<具体的版本号>  
    pull_policy: always
    restart: unless-stopped
    container_name: "peerbanhelper"
    volumes:
      - ./:/app/data
    ports:
      - "9898:9898"
    environment:
      - PUID=0
      - PGID=0
      - TZ=UTC
```

保存退出，执行命令 `sudo docker-compose up` 即可。WebUI 端口将在 9898 开放。

## 使用 Docker CLI 部署

**不推荐使用此方式部署，因为我们会频繁升级。如果您使用此方式部署，可能会极大增加您的维护负担（更新的时候您需要停止容器、删除容器再重新执行下面的 `docker run` 命令）。**

找一个合适的位置创建一个目录作为 PBH 的数据存放位置，并将工作目录切换到此位置。
执行命令：

```bash
sudo docker run -d --pull always --name peerbanhelper --stop-timeout -p 9898:9898 -v ${PWD}/:/app/data/ ghostchu/peerbanhelper:latest
# 若使用镜像源则不能使用 latest 标签，请使用具体版本号，否则可能会导致拉取到的镜像是远古版本
# sudo docker run -d --pull always --name peerbanhelper --stop-timeout -p 9898:9898 -v ${PWD}/:/app/data/ registry.cn-hangzhou.aliyuncs.com/ghostchu/peerbanhelper:<具体的版本号>
```

WebUI 端口将在 9898 开放。
