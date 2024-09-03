# 连接 BTN

要参与 BTN 计划，只需要将 BTN 客户端连接到 BTN 服务器就好了。本文使用 PeerBanHelper 作为 BTN 客户端，Sparkle 作为 BTN 服务端进行演示。

## Sparkle

Sparkle 是 PBH-BTN 的官方 BTN 服务器。

### 注册账号，创建 UserApp

浏览器打开 [https://btn-prod.ghostchu-services.top](https://btn-prod.ghostchu-services.top) 并使用 GitHub 授权登录，就会自动创建一个账号。  

点击顶部菜单的 “用户应用程序” 链接来到管理页面。

![homepage](./assets/btn-homepage.png)

点击 “创建新用户应用程序”，输入一个备注，然后点击按钮创建。

![management](./assets/userapp-management.png)

现在记下页面上显示的 `AppID` 和 `AppSecret`，因为一旦关闭这个页面，`AppSecret` 就不会再显示了。

![created](./assets/userapp-created.png)

## 在 PBH 上加入 BTN 网络

打开 `data/config/config.yml` 配置文件，找到下面的配置部分：

```yaml
# BitTorrent Threat Network 威胁防护网络（测试版）
# BitTorrent Threat Network (BETA)
btn:
  # 启用 BTN 模块
  # 启用后，才可以使用由 BTN 提供的云规则功能
  # 为了隐私起见，此功能需要您手动启用
  # Enable BTN module, all settings below will only take effects if you turn this on.
  enabled: false
  # 启用数据提交
  # BTN 网络基于所有启用此功能的用户提交的数据，对 Peers 进行可信度验证
  # 通过启用此选项，您也会加入 BTN 网络并提交您的 Torrent 上的活动
  # 以下信息将被发送到 BTN 实例；
  # 您的 Torrent 列表（包括：Torrent 种子摘要的二次不可逆哈希和 Torrent 大小）
  # 连接到您的 Torrent 的所有 Peers （包括：IP地址、端口号、PeerID、UserAgent（ClientName），Peer协议，Peer总下载量，Peer总上传量，Peer瞬时上传速度，Peer瞬时下载速度，Peer下载进度，以及您的下载器名称）
  # 封禁列表
  # Allow data submitting
  # If this option is enabled (and module also enabled), PBH will generate send data to BTN server including:
  # Your torrent lists (torrentIdentifier and torrent size, but not include: info hash, name)
  # All peers connected to torrents (Including: IP, Port, PeerID, UserAgent, Peer Protocol, Flags, Uploaded, Downloaded, UploadRate, DownloadRate, PeerProgress, YourProgress and Downloader Name)
  # Your banlist
  submit: true
  # 部分 BTN 实例可能要求您登录验证以确认您的身份或下发不同的配置文件。如果是这样的话，您需要在下面输入凭据信息
  # 如果 BTN 实例未要求您登录验证，则通常不需要填写
  # Some BTN instance may require your authentication, if so, you can fill the credentials here
  app-id: "example-app-id"
  app-secret: "example-app-secret"
  # 填写实例 URL，您需要自行寻找一个 BTN 实例服务器
  # 默认使用 PBH-BTN 社区 BTN 服务器，请前往 https://btn-prod.ghostchu-services.top 注册并获取一个账号
  # The BTN instance URL, you need find a BTN instance
  # By default, PBH-BTN official BTN instance will be used
  config-url: "https://btn-prod.ghostchu-services.top/ping/config"
```

`app-id` 填写你刚刚记下的 `AppId`，`app-secret` 也同理填写刚刚记下的 `AppSecret`。

`config-url` 是你的 BTN 服务器提供的链接，对于 Sparkle （官方 BTN 服务器）来说，这个链接是 `https://btn-prod.ghostchu-services.top/ping/config`。

最后别忘了把 `enabled: false` 改成 `enabled: true`，保存重启 PBH 就应成功加入了。
