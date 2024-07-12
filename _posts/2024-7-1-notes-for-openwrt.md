---
layout: post
title: 群晖中的openwrt
tags: [openwrt,群晖]
categories: 生活
giscus_comments: true
related_posts: true
date: 2024-7-1
toc:
  sidebar: left
---

## 群晖中安装openwrt

### 安装Virtual Machine Manager以及导入openwrt映像

安全起见，只安装旁路由形式的openwrt。

安装Virtual Machine Manager，打开虚拟机。选择网络，新建名称为wan的网口。

下载openwrt的img文件，上传到虚拟机-映像-硬盘映像，点击虚拟机-新增-导入，从硬盘映像导入，按部就班，直到设置CPU和内存，取大一点内存，在虚拟盘选择硬盘映像，点击齿轮，切换虚拟路由器工作模式从virto(半双工)到e100(全双工)。按部就班到完成，不要勾选自动启动。

开机，点击连接到openwrt，执行`vi /etc/config/network`，修改lan的ip地址到当前内网频段（建议为`192.168.1.2`），保存退出，执行`reboot`重启。

浏览器输入`192.168.1.2`，进入openwrt的管理界面，设置密码。

### OpenWrt旁路由配置

- DHCP的分配： 一般由主路由承担DHCP的分配，因此在“网络-接口-LAN”修改界面中将openwrt的DHCP关闭。
- IPv6设置：全部禁用
- 桥接接口：关闭


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <div>
            {% include figure.html path="assets/img/blog/openwrt/openwrt_lan_setting1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
        <div class="mt-3">
            {% include figure.html path="assets/img/blog/openwrt/openwrt_lan_setting2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
        </div>
        <div>具体lan口设置</div>
    </div>
</div>

- 诊断： 在左侧栏“网络-诊断”中，看是否能ping通。

### 主路由设置
主路由和旁路由需要互指对方的网关，旁路由的网关指向主路由的IP地址。一般情况下，`win+R`键入`control`，修改本地网络配置，使其DNS和网关指向旁路由的IP地址。

注意，互指不等同与真正的平等互指，网关和DNS的互指只会造成无穷无尽的循环。以及记得修改主路由的默认DNS，从当地运营DNS改为公共DNS（8.8.8.8或1.1.1.1）。

### 防火墙规则设置

对于一些比较高级的主路由（比如我的TPlinke 3200），其往往会有比较高级的防火墙规则，当其发现发送请求的ip（旁路由）与你实际上的ip（你的本机）不符时，就会怀疑你ip被劫持，丢掉这个请求。

具体表现为：所有代理的请求可以正常访问，但是直连的请求无法访问。因为后者没有做伪装，更容易被辨别。

解决方法为，修改旁路由的防火墙规则，将`iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE `加入到防火墙规则中，重启防火墙，同时关闭LAN口桥接（之前已经做过了）。

### DNS分流设置

因为所有的旁路由的科学插件都是对v2ray的拙劣模仿，其DNS方面的加密做得不是很好，需要自己手动设置。一些运营商的DNS服务器可以很轻易污染到你的请求，具体表现为`nslookup`结果与实际ip不符，我个人的做法是重定向dnsmasq的53端口到ADguardHome(不是重写，经测试不稳定，尽管原理是应该会响应更快一点),同时将规则改回只基于域名的分流asls。

ADguardHome的DNS设置为(尽量选用加密的而非直接的DNS)：

```
# 下面的 DNS 组合供选择，选择延迟较低的
# Google DNS
tls://8888.google
tls://dns.google
tls://dns.google.com
https://dns.google/dns-query
https://dns.google.com/dns-query
https://8888.google/dns-query
h3://dns.google/dns-query
h3://dns.google.com/dns-query
h3://8888.google/dns-query
# OpenDNS
tls://dns.opendns.com
https://doh.opendns.com/dns-query
# Quad9 DNS
tls://dns11.quad9.net
https://dns11.quad9.net/dns-query
# AdGuard DNS
tls://dns.AdGuard-dns.com
https://dns.AdGuard-dns.com/dns-query
quic://dns.AdGuard-dns.com
h3://dns.AdGuard-dns.com/dns-query
# NextDNS
tls://dns.nextdns.io
https://dns.nextdns.io/dns-query
quic://dns.nextdns.io
h3://dns.nextdns.io/dns-query
# 欧盟 DNS
https://zero.dns0.eu/
tls://zero.dns0.eu
quic://zero.dns0.eu
#国内
[/quark.cn/]quic://dns.alidns.com
[/sobereva.com/]quic://dns.alidns.com
```

Bootstrap DNS服务器（用来解析DNS的DNS）：

```
tls://223.5.5.5
quic://223.5.5.5
tls://1.12.12.12
```
