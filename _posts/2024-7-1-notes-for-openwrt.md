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
