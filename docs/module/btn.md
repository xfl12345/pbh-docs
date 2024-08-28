# BTN 云端规则

使用来自 BTN 网络的云端规则。需要提前配置 PBH 接入 BTN。

## 配置文件

```yaml
  # 启用来自 BTN 网络的规则
  # Enable the network rules from BTN server, only works when you configured BTN server in config.yml
  btn:
    enabled: true
    # 封禁时间，单位：毫秒，使用 default 则跟随全局设置
    ban-duration: 259200000
```