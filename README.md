<h1 align="center"> ✈️基于mihomo内核代理程序<br> <br>配置模板</h1>

---

<p align="center"><b>😂探讨用于Windows Clash Verge、ASUS MerlinClash、OpenWrt Nikki、OpenClash等mihomo内核代理程序的yaml配置模板😂</b></p>
<p align="center"><b>🐜持续漏网之鱼🐟的维护补录，定制个人需求🐜</b></p>

---
* [📌 前言](#-前言)
* [⚡ Mihomo通用yaml模板](#-Mihomo通用yaml模板)
* [⚙️ 特殊需求](#-特殊需求)


## 📌 前言

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;家庭网络遵循简单好用，例如仅一台硬路由也能满足家庭上网需求。广告拦截可简单的规则拦截，其他复杂拦截功能尽量不要放置在代理程序中，在终端安装例如AdGuard插件效果远远好于诸如OpenClash的广告拦截效果。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;通过对比ClashVerge、MerlinClash、OpenClash、Nikki等代理程序，各种程序在不同的硬件和网络环境各有优劣：有稳定的旁路由（一般为7×24小时开机的独立旁路由），使用OpenClash、Nikki等比较稳定；如果旁路由需经常开关机，那部署在主路由上比较合适（如OpenClash、Nikki或Merlinclash等）；科学上网需求不大的，在终端电脑上安装类似Clash Verge的代理程序，随用随开。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 到底什么配置文件才好用？在YouTube上很多大佬的配置教程，他们用的机场本身质量就非常好，怎么选节点都好用，但同一配置模板当换成质量差的机场时就不好用了，往往在实际使用中，ping的高低并不等于连接速率，有时选择ping低的节点，却十分卡顿。本项目在merlinclash、openclash、nikki、clashverge长时测试，merlinclash为主路由，openclash和nikki为旁路由，采用两个廉价机场长时验证，十分稳定，可实现长期免维护。

#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本项目仅提供基于Mihomo的配置文件示例，分流规则参照[Aethersailor/Custom_OpenClash_Rules](https://github.com/Aethersailor/Custom_OpenClash_Rules)项目优化而来，各代理程序的设置可自行查阅相关教程，如OpenClash的设置可参照 Aethersailor的[设置方案](https://github.com/Aethersailor/Custom_OpenClash_Rules/wiki/OpenClash-%E8%AE%BE%E7%BD%AE%E6%96%B9%E6%A1%88)🥊。另外[HenryChiao](https://github.com/HenryChiao/MIHOMO_YAMLS/tree/main/THEYAMLS/General_Config)收集了全网做的较好的yaml配置模板，可集思广益参考借鉴。
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;有好建议敬请Issues反馈探讨。

***

-  ## ⚡ Mihomo通用yaml模板
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;配置模板适用于Mihomo内核的代理程序，如OpenClash、Nikki、Merlinclash、Clash Verge等，可直接导入模板使用或稍加改动即可。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 配置模板最多采用了五层策略，层次功能分明，故转层负责检测和确保节点可用，地区策略层负责节点选择的形式，节点选择方式有均衡、自动、smart、手动，所有故障转移均不直接选择最底层节点，而是地区策略组之间故障转移，如：故转-手动→全球手动→地区策略→均衡or自动（或smart）or手动→机场节点，“全球手动”可自定义选择喜欢的地区策略或单一节点，当"全球手动"的节点失联时，自动切换至可用节点，闲时几乎不产生代理流量，响应迅速，可实现长时免维护。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 规则来源主要是mihomo官方数据库，一个是采用mihomo内置GEOSITE和GEOIP数据库，另一个是采用的[MetaCubeX](https://github.com/gog-xie/meta-rules-dat/tree/meta/geo)大佬实时更新的GEO数据库，配置中内置了分区域节点的smart智能选择、自动选择、手动选择、故障转移、负载均衡等功能，仅需修改yaml文件中的机场地址和名称即可。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 各种配置大同小异，Pro和Plus类配置模板可实现指定机场分流出站，其余模板均是多机场节点混用出站。Plus采用多元故转默认地区界节点，可实现更为灵活的分流策略。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 系统上线后按自己需求选择好分流策略即可使用，控制面板中各个策略和节点连通性是否绿色的其实无关紧要，不用强迫症的不停点击测试连通性，系统会根据相关规则设定去判定节点的选择。

<div align="center">


| <div align="center">☑️</div> | <div align="center">🧮配置文件</div> | <div align="center">🥇推荐指数</div> | <div align="center">📈配置详情</div> | <div align="center">📑特点</div> |
| :--- | :--- | :--- | :--- | :--- |
| <div align="center">**1**</div> | 📄**RuleAIO.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/RuleAIO.yaml)</div> | 多机场混合出站 |
| <div align="center">**2**</div> | 📄**RuleAIOPro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/RuleAIOPro.yaml)</div> | 多机场**自定义**出站 |
| <div align="center">**3**</div> | 📄**RuleAIOPlus.yaml** | 🥇★★★★☆ | <div align="center">[跳转](yaml/RuleAIOPlus.yaml)</div> | 多机场**混合**或**自定义**出站，**多元**默认故转 **${\color{blue}\text{【推荐】}}$** |
| <div align="center">**4**</div> | 📄**RuleLite.yaml** | 🥉★★★ | <div align="center">[跳转](yaml/RuleLite.yaml)</div> | 极简分流，多机场混合出站
| <div align="center">**5**</div> | 📄**RuleLitePro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/RuleLitePro.yaml)</div> | 极简分流，多机场**自定义**出站  **${\color{blue}\text{【推荐】}}$** |
| <div align="center">**6**</div> | 📄**RuleSmartAIO.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/RuleSmartAIO)</div> | 适配Smart核心，多机场混合出站 |
</div>

***  

-  ## ⚓ 特殊需求
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;科学插件部署在主路由的场景，常常有部分设备不需要科学代理，旁路由比较好设置，只需让需要代理设备的网关指向旁路由，不需代理的默认指向主路由即可；但也有设备仅少量代理需求，其余不走科学代理。特别是前者比较特殊，既要少量代理，又要大部分直连，比如白群仅docker镜像库、Emby海报刮削需要科学代理，其余全部绕过内核走直连的情况（主要是群晖按普通规则代理后，可能会产生不必要的代理流量，实际上是不需要的），可以利用规则先后顺序正则匹配的特点来实现部分代理的要求，按先后顺序匹配指令，如果上位规则没有匹配上，则匹配下一项规则。根据这一特点，先将这类设备IP 与MAC地址绑定，再让不需代理的设备IP匹配走直连，其次让部分需要代理的设备IP 匹配Proxy规则，最后让部分需要代理的设备IP匹配走直连，把这三项放规则集的最前端即可。例如以下规则：

```
rules:

# DHCP的192.168.1.101 ~ 199 范围所有设备走直连，即使访客连入网络也不会走代理
- SRC-IP-CIDR,192.168.1.101/32,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.102/31,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.104/30,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.108/30,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.112/28,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.128/26,DIRECT,no-resolve
- SRC-IP-CIDR,192.168.1.192/29,DIRECT,no-resolve

# 内网MAC绑定设备192.168.1.88所有链接走直连，设备192.168.1.98的部分链接（My_Proxy）走代理，其余走直连
- SRC-IP-CIDR,192.168.1.88/32,DIRECT,no-resolve
- RULE-SET,My_Proxy,默认代理
- SRC-IP-CIDR,192.168.1.98/32,DIRECT,no-resolve
- SRC-IP-SUFFIX,::abcd:1234:efgh:5678/64,DIRECT,no-resolve  #某内网设备通过IPV6地址实现部分代理其余直连，由于路由器重启后IPV6前四段会变化，但后四段是根据MAC地址生成的，匹配后缀即可
......

```

                     
---
