# xray
compile xray and install ,just move xray to /usr/bin/ is ok
and rename xray to v2ray
# in stall xray service
sudo gedit /etc/systemd/system/v2ray.service
add contents as following
```
[Unit]
Description=V2Ray Service
After=network.target nss-lookup.target

[Service]
User=nobody
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE
ExecStart=/usr/bin/v2ray -confdir /etc/v2ray/

[Install]
WantedBy=multi-user.target
```

then start service
sudo service v2ray start


# v2sub

Go 编写的用于 linux 下订阅并简单配置 [v2ray](https://github.com/v2ray/v2ray-core) 的命令行工具。

程序会创建 `/etc/v2sub.json` 文件用于存储订阅信息。

使用前需确保 v2ray.service 服务已注册且默认 v2ray 配置文件路径为 `/etc/v2ray.json`。

## Features

+ 内置配置文件和代理规则，默认监听 socks \[1081\] 和 http \[1082\]
+ icmp ping 测试节点延迟
+ ~~可更新代理规则~~ 内置代理规则使用DNS分流+白名单
+ 支持 VMess / SS / [Trojan](https://github.com/trojan-gfw/trojan) 订阅与配置

![v2sub](https://github.com/arkrz/v2sub/raw/master/v2sub.png)

## Usage

因 ping 与 服务重启 权限需要，以 root 权限运行:

```shell
sudo v2sub
```

快速切换节点：

```shell
sudo v2sub -q
```

允许监听外部连接：

```shell
sudo v2sub -wan
```

修改监听端口：

```shell
sudo v2sub -http 7890 -socks 7891
```

更多帮助：

```shell script
v2sub -help
```

## Note

trojan 功能通过 v2ray 转发实现，因此可以使用规则代理。使用前需确保 trojan.service 服务已注册且默认配置文件路径为 `/etc/trojan.json`。

## Warning

程序会覆盖 v2ray 配置文件。

This tool will truncate your v2ray config.
