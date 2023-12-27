---
date: 2023-12-28 06:41
title: zerotier组网
tags:
  - 网络
  - 内网穿透
---
设备: mac,刷了openwrt的路由器(redmi_ac2100)

### 1.注册zerotier账户,并创建网络
官网:[https://my.zerotier.com](https://my.zerotier.com/)

注册后点击create a network,下方table处会新增一行数据,点击进入
![](../../assets/Pasted%20image%2020231228065504.png)
进入页面后networkid很重要,name随意起一个,access control选择private
![](../../assets/Pasted%20image%2020231228065648.png)
向下翻,选择地址.建议不要和路由器内网的网段类似,比如,都是192.168.x.y/24,理论上x不同不会有问题,实际上后续访问路由器下其他设备时可能会有问题.
![](../../assets/Pasted%20image%2020231228065824.png)

### 2.组网设备设置
此处以mac举例,移动端,win端,linux端操作类似

在网络页面顶部,点击download,根据设备下载对应版本
![](../../assets/Pasted%20image%2020231228070200.png)
![](../../assets/Pasted%20image%2020231228070338.png)
软件安装完毕后,在mac上是这个样子
![](../../assets/Pasted%20image%2020231228070553.png)
点击join new network ,在输入框中填入networkid
![](../../assets/Pasted%20image%2020231228070659.png)
之后该设备就加入了虚拟网.回到zt的网络管理页面,在下方members中可以看到有新设备接入.
将auth列的复选框勾选上,此时该设备才算正式接入网络. 可以在name/desc中填写主机名称和描述,也可在managed ips列自行添加主机虚拟ip
![](../../assets/Pasted%20image%2020231228070905.png)

### 3.路由器启用zerotier
我的路由器刷系统时用的是懒人包,已经自带zerotier插件.刷机与插件安装就自行ググる一下吧.
进入路由管理页面后,打开zt插件管理页面,点击启用,然后填入network id并点击加号添加,勾选自动允许客户端nat,最后点击保存并应用.
![](../../assets/Pasted%20image%2020231228071548.png)
此时仍回到zt网络管理页面,可以看到路由器已经加入网络.同样勾选auth,此时在mac上应该已经可以ping通路由器.(ping虚拟地址不是lan地址)

### 4.添加内网映射
只能访问到路由还是まだまだ,接下来我们要添加路由,使mac能访问到路由器下其他设备.

回到zt管理页面,在之前选择网段的上方,可以添加路由.
destination内填写路由器lan网段,via填写路由器虚拟地址.
比如,我路由器局域网网段为192.168.50.0/24,路由虚拟ip为10.147.18.3,则分别填写到输入框内,然后点击submit添加路由.
![](../../assets/Pasted%20image%2020231228072117.png)
然后ping一下局域网下设备(使用实际局域网地址)
至此,大功告成!
了,吗?

你会发现大概率你还是不能从mac ping到路由下设备(如果能ping到,确认下你是不是本身就连在同一局域网下,当然,能ping到更好)

你可能还要在路由器上输入如下指令:
```bash
route add -net <虚拟网段> dev br-lan
iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
```
这回再尝试应该就可以成功了