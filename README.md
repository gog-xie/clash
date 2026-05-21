<h1 align="center"> ✈️基于mihomo内核代理程序<br>⠀<br>订阅配置说明</h1>

---

<p align="center"><b>😂探讨用于Windows Clash Verge、ASUS MerlinClash、OpenWrt Nikki、OpenClash等mihomo内核代理程序的yaml配置模板😂</b></p>
<p align="center"><b>🐜持续漏网之鱼🐟的维护补录，定制个人需求，如个别内网设备指定域名代理，其余直连的特殊需求🐜</b></p>

---

- ## 1 前言
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;科学上网常常部署在旁路由，但旁路由时而会出现莫名的小问题，DHCP也有不便之处。其实家庭网络简单好用即可，仅一台硬路由也能满足家庭上网需求，如安装Merlinclash，实现国内外科学分流，沿用了Openclash的配置文件，效果还是挺好！接近无感科学上网，但路由硬件高一点比较好，试用BE86U开启MerlinClash后，不同的配置模板使用效果不一，有的模版会偶尔卡死自动重启。另外，广告拦截尽量不要放置在代理程序中，在终端安装例如AdGuard插件效果远远好于诸如OpenClash的广告拦截效果。
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通过对比ClashVerge、MerlinClash、OpenClash、Nikki等代理程序，各种程序在不同的硬件和网络环境各有优劣：有稳定的旁路由（一般为7×24小时开机的独立旁路由），使用OpenClash、Nikki等比较稳定；如果旁路由需经常性的开关机，那部署在主路由上比较合适（如OpenClash、Nikki或Merlinclash等）；科学上网需求不大的，在终端电脑上安装类似ClashVerge的代理程序，随用随开。
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目主要是相关订阅模板的下载，各代理程序的设置请自行查阅相关教程，如OpenClash的设置建议参照 [Aethersailor](https://github.com/Aethersailor/Custom_OpenClash_Rules/wiki/OpenClash-%E8%AE%BE%E7%BD%AE%E6%96%B9%E6%A1%88)大佬的设置方案🥊。另外[HenryChiao](https://github.com/HenryChiao/MIHOMO_YAMLS/tree/main/THEYAMLS/General_Config/HenryChiao)大佬收集了全网做的较好的yaml模板，可集中参考借鉴

***

- ## 2 OpenClash订阅模板

- ### 2.1 openclash等通用模板（推荐）

#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;采用Subconverter订阅时有小毛病出现，用yaml配置文件导入可减少小问题，而且可配置较为美观的Zashboard控制面板。下载yaml文件后只需输入机场名称和机场订阅地址后导入OpenClash即可。

#### [2.1.1 综合模板](https://github.com/gog-xie/Clash/blob/main/yaml/OpenClash/MihomoGOG)

```
https://github.com/gog-xie/Clash/blob/main/yaml/OpenClash/MihomoGOG
```


-  ## 3 其他系统yaml模板
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;若主路由为华硕硬路由，配置MerlinClash订阅规则完全可借鉴OpenClash的订阅模板，可直接导入模板使用或稍加改动即可。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在OpenClash配置订阅中的规则集选择“启用”，避免yaml文件太大影响速度，再到配置管理中下载yaml配置文件导入Merlinclash中可直接使用。目前Merlinclash中GoeIP数据库数量为0，官方解释为“mmdb等格式的geo文件无法统计数量”，但GoeSite和GoeIP数据正常调用，使用效果不受影响。同理，也可导入Windows Clash Verge中使用，导入Nikki时注意需带相关设置参数。这里推荐使用以下yaml文件，仅需修改yaml文件中的机场地址和名称即可：


#### [3.1.1 ClashVerge综合模板](https://github.com/gog-xie/Clash/blob/main/yaml/ClashVerge/ClashVerge_GOG)（可引用Openclash的模板）

```
https://github.com/gog-xie/Clash/blob/main/yaml/ClashVerge/ClashVerge_GOG
```

#### [3.1.2 MerlinClash综合模板（推荐）](https://github.com/gog-xie/Clash/blob/main/yaml/MerlinClash/GOGAIO)

```
https://github.com/gog-xie/Clash/blob/main/yaml/MerlinClash/GOGAIO
```


#### [3.1.4 Nikki综合模板（推荐）](https://github.com/gog-xie/Clash/blob/main/yaml/Nikki/MihomoForNikki)

```
https://github.com/gog-xie/Clash/blob/main/yaml/Nikki/MihomoForNikki
```

<p align="center"> <b>MerlinClash GeoIP数量显示为0 </b></p>
<div align="center"> <img src="https://github.com/gog-xie/Clash/blob/main/pic/clash/merlinclash%E5%86%85%E7%BD%AE%E8%A7%84%E5%88%99%E8%B0%83%E7%94%A8.png" width="360" heiht="190"></div>

-  ## 4 特殊需求
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在OpenClash、Nikki或MerlinClash系统中，常常有部分设备不需要科学代理，旁路由比较好设置，只需让需要代理设备的网关指向旁路由，不需代理的默认指向主路由即可；但也有设备仅少量代理需求，其余不走科学代理，或openclash安装在主路由情况下部分设备不走科学代理。特别是前者比较特殊，既要少量代理，又要大部分直连，比如白群仅docker镜像库、Emby海报刮削需要科学代理，其余全部绕过内核走直连的情况（主要是群晖按普通规则代理后，经常性的产生不必要的代理流量，实际上是不需要的），可以利用规则先后顺序正则匹配的特点来实现部分代理其他不代理，按先后顺序匹配指令，如果没有匹配上，再去匹配下一项规则。根据这一特点，先将这类设备IP 与MAC地址绑定，再让不需代理的设备IP匹配走直连，其次让部分需要代理的设备IP 匹配Proxy规则，最后让部分需要代理的设备IP匹配走直连，把这三项放规则集的最前端即可。例如以下规则：

```
rules:

# 192.168.1.101 ~ 199 所有设备走直连
- SRC-IP-CIDR,192.168.1.101/32,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.102/31,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.104/30,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.108/30,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.112/28,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.128/26,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.192/29,DIRECT,no-resolve

# 内网设备192.168.1.88所有链接走直连，设备192.168.1.98的部分链接（My_Proxy）走代理，其余走直连
- SRC-IP-CIDR,192.168.1.88/32,DIRECT,no-resolve
- RULE-SET,My_Proxy,手动选择
- SRC-IP-CIDR,192.168.1.98/32,DIRECT,no-resolve
- SRC-IP-CIDR,240e:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx/128,DIRECT,no-resolve  #某内网设备通过IPV6地址实现部分代理其余直连
......

```

                     
***

<p align="center"> <b>手机端Zashboard控制面板效果 </b></p>
<div align="center"> <img src="https://github.com/gog-xie/Clash/blob/main/pic/clash/zashboard3.png?raw=true" width="256" heiht="560"></div>

---

<p align="center"> <b>电脑端Zashboard控制面板局部效果 </b></p>
<div align="center"> <img src="https://github.com/gog-xie/Clash/blob/main/pic/clash/zashboard1.png?raw=true" width="720" heiht="380"></div>

---

<p align="center"> <b>电脑端Zashboard控制面板分流策略组 </b></p>
<div align="center"> <img src="https://github.com/gog-xie/Clash/blob/main/pic/clash/zashboard2.png?raw=true" width="720" heiht="380"></div>

---

<p align="center"> <b>电脑端Zashboard控制面板连接列表 </b></p>
<div align="center"> <img src="https://github.com/gog-xie/Clash/blob/main/pic/clash/zashboard4.png" width="1080" heiht="760"></div>

---

<p align="center"> <b>电脑端Zashboard控制面板连接详情 </b></p>
<div align="center"> <img src="https://github.com/gog-xie/Clash/blob/main/pic/clash/zashboard5.png" width="1080" heiht="760"></div>

---
