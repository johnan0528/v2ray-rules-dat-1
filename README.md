# v2ray-rules-dat
# 新版V2rayN的路由规则设置
>本项目修改于[@Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) 。因原项目的规则文件格式过于落后，导致无法导入新版的V2rayN中使用，故更新其Whitelist白名单、Blacklist黑名单和DNS setting DNS设置文件的格式，并在其基础上进行更新和改进，以便小白能够设置自己的新版V2ray的代理规则。更多规则细节请访问原项目地址，在本项目中不多赘述。想要了解V2rayN的更多高级用法请访问v2rayN的项目[@2dust/v2rayN](https://github.com/2dust/v2rayN) ，在本项目中也不过多赘述。

* 下载最新版v2rayN请访问https://github.com/2dust/v2rayN/releases
* 了解原项目作者的规则请访问https://github.com/Loyalsoldier/v2ray-rules-dat/releases

## 依赖GEO文件

>使用本项目的路由规则前，请先下载加强版的`geoip.dat`和`geosite.dat`，并导入到v2rayN客户端的目录，替换原来的`geoip.dat`和`geosite.dat`。下载地址：

* `geoip.dat`

墙内：https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geoip.dat

墙外：https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat （比墙内先更新）

* `geosite.dat`

墙内：https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geosite.dat

墙外：https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat （比墙内先更新）

## 路由配置如下设置
首先需要开启v2rayN路由设置中的启用路由高级功能，随后双击需要编辑的规则，在弹出的窗口上方菜单栏选择导入规则-从剪贴板导入规则

当然，如果你有自己的需求，也懂得如何编辑代码，完全可以对以下路由规则进行修改。如果你希望修改geo配置文件，请访问https://github.com/Loyalsoldier/geoip
### 绕过大陆（白名单Whitelist）
绕过大陆，即所有服务器和ip在中国大陆的网站优先使用本地网络直接连接，所有其他的域名均使用vpn进行连接
```
[
  {
    "port": "",
    "outboundTag": "proxy",
    "ip": [],
    "domain": [
      "geosite:geolocation-!cn",
      "github.com",
      "githubassets.com",
      "githubusercontent.com",
      "store.steampowered.com"
    ],
    "protocol": []
  },
  {
    "type": "field",
    "outboundTag": "block",
    "domain": [
      "mousegesturesapi.com",
      "cf-se.com",
      "geosite:category-ads-all",
      "googleads.g.doubleclick.net",
      "adservice.google.com"
    ]
  },
  {
    "type": "field",
    "port": "",
    "outboundTag": "direct",
    "ip": [
      "geoip:private",
      "geoip:cn",
    ],
    "domain": [
      "bitwarden.com",
      "bitwarden.net",
      "gravatar.com",
      "gstatic.com",
      "letsencrypt.org",
      "adblockplus.org",
      "safesugar.net",    
      "geosite:private",
      "geosite:cn",
      "geosite:adobe",
      "geosite:adobe-activation",
      "geosite:microsoft",
      "geosite:msn",
      "geosite:apple",
      "geosite:private",
      "geosite:apple-cn",
      "geosite:google-cn",
      "geosite:tld-cn",
      "geosite:category-games@cn"
    ],
    "protocol": []
  },
  {
    "type": "field",
    "port": "0-65535",
    "outboundTag": "proxy"
  }
]
```
### 黑名单（Blacklist）
黑名单，即老版本v2rayN中的PAC连接，只有已知被墙的网站优先走vpn，其余所有网站（不管境内境外）均通过本地网络直连
```
[
  {
    "outboundTag": "proxy",
    "domain": [
     "geosite:gfw",
     "geosite:greatfire",
    ]
  },
  {
    "outboundTag": "block",
    "domain": [
      "geosite:category-ads-all",
      "mousegesturesapi.com"
    ]
  },
  {
   "type": "field",
   "outboundTag": "Proxy",
   "ip": ["geoip:telegram"]
  },
  {
    "type": "field",
    "port": "0-65535",
    "outboundTag": "direct"
  }
]
```

## DNS配置如下设置
设置-参数设置-DNS设置-直接curl+v粘贴规则
```
{
  "hosts": {
    "dns.google": "8.8.8.8",
    "dns.pub": "119.29.29.29",
    "dns.alidns.com": "223.5.5.5",
    "geosite:category-ads-all": "127.0.0.1",
    "dns.cloudflare.com": "1.1.1.1",
    "aws.amazon.com":"169.254.169.253"
  },
  "servers": [
    {
      "address": "https://1.1.1.1/dns-query",
      "domains": ["geosite:geolocation-!cn"],
      "expectIPs": ["geoip:!cn"]
    },
    "8.8.8.8",
    {
      "address": "114.114.114.114",
      "port": 53,
      "domains": ["geosite:cn", "geosite:category-games@cn"],
      "expectIPs": ["geoip:cn"],
      "skipFallback": true
    },
    {
      "address": "localhost",
      "skipFallback": true
    }
  ]
}
```

# 项目资料引用
[@Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)

[@2dust/v2rayN](https://github.com/2dust/v2rayN)

https://ivpsr.com/281.html

https://www.v2fly.org/config/dns.html#dnsobject

# 鸣谢
[@Loyalsoldier](https://github.com/Loyalsoldier)

[@2dust](https://github.com/2dust)
