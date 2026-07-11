<h1 align="center"> ✈️基于mihomo内核代理程序<br>⠀<br>配置模板</h1>

---

<p align="center"><b>😂探讨用于Windows Clash Verge、ASUS MerlinClash、OpenWrt Nikki、OpenClash等mihomo内核代理程序的yaml配置模板😂</b></p>
<p align="center"><b>🐜持续漏网之鱼🐟的维护补录，定制个人需求🐜</b></p>

---

- ## 1 前言
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;科学上网常常部署在旁路由，但旁路由时而会出现莫名的小问题，DHCP也有不便。其实家庭网络简单好用即可，仅一台硬路由也能满足家庭上网需求，在主路由BE86U安装Merlinclash，实现国内外科学分流，几乎可实现无感内外网。另外，广告拦截尽量不要放置在代理程序中，在终端安装例如AdGuard插件效果远远好于诸如OpenClash的广告拦截效果。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通过对比ClashVerge、MerlinClash、OpenClash、Nikki等代理程序，各种程序在不同的硬件和网络环境各有优劣：有稳定的旁路由（一般为7×24小时开机的独立旁路由），使用OpenClash、Nikki等比较稳定；如果旁路由需经常性的开关机，那部署在主路由上比较合适（如OpenClash、Nikki或Merlinclash等）；科学上网需求不大的，在终端电脑上安装类似Clash Verge的代理程序，随用随开。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 折腾卵路由这么久，到底什么配置文件才好用？YouTube很多大佬教程，他们的机场质量非常好，同一配置模板当换成质量差的机场时就不好用了，特别是喜欢采用url-test节点选择模式，往往在实际使用中，ping的高低并不等于连接速率，往往选择ping低的节点，却十分卡顿。作者以华硕路由器BE86U作主路由，采用梅林改版固件，在Merlinclash采用了本配置的yaml文件，购买了两个廉价机场，经长时间验证，十分稳定，可实现长期免维护。

#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目仅提供基于mihomo的配置文件示例，各代理程序的设置请自行查阅相关教程，如OpenClash的设置可参照 [Aethersailor](https://github.com/gog-xie/Custom_OpenClash_Rules/blob/main/wiki/1.OpenClash-%E8%AE%BE%E7%BD%AE%E6%96%B9%E6%A1%88.md)大佬的设置方案🥊。另外[HenryChiao](https://github.com/gog-xie/MIHOMO_YAMLS/blob/main/THEYAMLS/General_Config/gog-xie/RuleAIOPro.yaml)大佬收集了全网做的较好的yaml配置模板，可集思广益参考借鉴。

***

-  ## 2 Mihomo通用yaml模板
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本配置yaml模板适用于Mihomo内核的代理程序，如OpenClash、Nikki、Merlinclash、Clash Verge等，可直接导入模板使用或稍加改动即可。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.1 配置模板最多采用了五层策略，层次功能分明，故转层负责检测和确保节点可用，地区策略层负责节点选择的形式，节点选择方式有均衡、自动、smart、手动，所有故障转移均不直接选择最底层节点，而是地区策略组之间故障转移，如：故转-手动→全球手动→地区策略→均衡or自动（或smart）or手动→机场节点，“全球手动”可自定义选择喜欢的地区策略或单一节点，当"全球手动"的节点失联时，自动切换至可用节点，闲时几乎不产生代理流量，响应迅速，可实现长时免维护。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2 规则来源主要是mihomo官方数据库，一个是采用mihomo内置GEOSITE和GEOIP数据库，另一个是采用的[MetaCubeX](https://github.com/gog-xie/meta-rules-dat/tree/meta/geo)大佬实时更新的GEO数据库，配置中内置了分区域节点的smart智能选择、自动选择、手动选择、故障转移、负载均衡等功能，仅需修改yaml文件中的机场地址和名称即可。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.3 各种配置大同小异，Pro和Plus类配置模板可实现指定机场分流出站，其余模板均是多机场节点混用出站。Plus采用多元故转默认地区界节点，可实现更为灵活的分流策略。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.4 在控制面板中，总想所有节点ping都是绿色的，有点强迫症，其实绿色还是灰色无关大雅，系统上线后按自己需求选择好分流策略即可使用，系统是根据相关规则设定去判定节点的选择。

<div align="center">


| <div align="center">☑️</div> | <div align="center">🧮配置文件</div> | <div align="center">🥇推荐指数</div> | <div align="center">📈配置详情</div> | <div align="center">📑特点</div> |
| :--- | :--- | :--- | :--- | :--- |
| <div align="center">**1**</div> | 📄**GeoAIO.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/GeoAIO.yaml)</div> | 多组分流，自定义故转默认节点，多机场混合出站 |
| <div align="center">**2**</div> | 📄**GeoAIOPro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/GeoAIOPro.yaml)</div> | 多组分流，自定义故转默认节点，多机场自定义出站 |
| <div align="center">**3**</div> | 📄**GeoLite.yaml** | 🥉★★☆ | <div align="center">[跳转](yaml/GeoLite.yaml)</div> | 极简分流，自定义故转默认节点，多机场混合出站 |
| <div align="center">**4**</div> | 📄**GeoLitePro.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/GeoLitePro.yaml)</div> | 极简分流，自定义故转默认节点，多机场自定义出站 |
| <div align="center">**5**</div> | 📄**GeoSmartAIO.yaml** | 🥉★★★ | <div align="center">[跳转](yaml/GeoSmartAIO.yaml)</div> | 内置Geo数据库，适配Smart核心 |
| <div align="center">**6**</div> | 📄**RuleAIO.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/RuleAIO.yaml)</div> | 多组分流，自定义故转默认节点，多机场混合出站 |
| <div align="center">**7**</div> | 📄**RuleAIOPlus.yaml** | 🥇★★★★☆ | <div align="center">[跳转](yaml/RuleAIOPlus.yaml)</div> | 多机场**自定义**出站，**多元**默认故转 **${\color{blue}\text{【推荐】}}$** |
| <div align="center">**8**</div> | 📄**RuleAIOPro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/RuleAIOPro.yaml)</div> | 多组分流，多机场**自定义**出站 |
| <div align="center">**9**</div> | 📄**RuleLite.yaml** | 🥉★★★ | <div align="center">[跳转](yaml/RuleLite.yaml)</div> | 极简分流，多机场混合出站
| <div align="center">**10**</div> | 📄**RuleLitePro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/RuleLitePro.yaml)</div> | 极简分流，多机场**自定义**出站  **${\color{blue}\text{【推荐】}}$** |
| <div align="center">**11**</div> | 📄**RuleSmartAIO.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/RuleSmartAIO)</div> | 官方实时Geo数据库，适配Smart核心 |
</div>

***  

-  ## 3 特殊需求
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;科学插件部署在主路由的场景，常常有部分设备不需要科学代理，旁路由比较好设置，只需让需要代理设备的网关指向旁路由，不需代理的默认指向主路由即可；但也有设备仅少量代理需求，其余不走科学代理。特别是前者比较特殊，既要少量代理，又要大部分直连，比如白群仅docker镜像库、Emby海报刮削需要科学代理，其余全部绕过内核走直连的情况（主要是群晖按普通规则代理后，可能会产生不必要的代理流量，实际上是不需要的），可以利用规则先后顺序正则匹配的特点来实现部分代理其他不代理，按先后顺序匹配指令，如果没有匹配上，再去匹配下一项规则。根据这一特点，先将这类设备IP 与MAC地址绑定，再让不需代理的设备IP匹配走直连，其次让部分需要代理的设备IP 匹配Proxy规则，最后让部分需要代理的设备IP匹配走直连，把这三项放规则集的最前端即可。例如以下规则：

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
- RULE-SET,My_Proxy,默认代理
- SRC-IP-CIDR,192.168.1.98/32,DIRECT,no-resolve
- SRC-IP-SUFFIX,::abcd:1234:efgh:5678/64,DIRECT,no-resolve  #某内网设备通过IPV6地址实现部分代理其余直连，由于路由器重启后IPV6前四段会变化，但后四段是根据MAC地址生成的，匹配后缀即可
......

```

                     
---
