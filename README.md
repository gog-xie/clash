<h1 align="center"> ✈️基于mihomo内核代理程序<br> <br>配置模板</h1>

---

<p align="center"><b>😂探讨用于Windows Clash Verge、ASUS MerlinClash、OpenWrt Nikki、OpenClash、ClashMate等mihomo内核代理程序的yaml配置模板😂</b></p>
<p align="center"><b>🐜持续漏网之鱼🐟的维护补录，定制个人需求🐜</b></p>

---
* [📌 前言](#-前言)
* [🚫 关于广告拦截](#-关于广告拦截)
* [⚡ Mihomo通用yaml模板](#-Mihomo通用yaml模板)
* [⚓ 特殊设置](#-特殊设置)

---
## 📌 前言

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;家庭网络遵循简单好用，例如仅一台硬路由也能满足家庭科学上网需求，不必搞几层路由。通过对比ClashVerge、MerlinClash、OpenClash、Nikki、ClashMate等代理程序，各种程序在不同的硬件和网络环境各有优劣：有稳定的旁路由（一般为7×24小时开机的独立旁路由），使用OpenClash、Nikki等比较稳定；如果旁路由需经常开关机，那部署在主路由上比较合适（如OpenClash、Nikki或Merlinclash等）；科学上网需求不大的，在终端电脑上安装类似Clash Verge的代理程序，随用随开。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ini订阅配置文件简单实用，而yaml配置文件通用性较强，适用于各种mihomo代理程序，导入即用，各有千秋；到底什么配置文件才好用？在YouTube上很多大佬的配置教程，他们用的机场本身质量就非常好，怎么选节点都好用，同一配置模板当换成质量相对不稳定的机场时就不好用了，往往在实际使用中，ping的高低并不等于连接速率，有时选择ping低的节点，却十分卡顿，采用多个节点尝试连接，选择到连接速率最高节点概率将大幅度增加。另一方面，每个人上网习惯不同，有些小众网站分流，对于某些人来讲确是经常使用的分流，只有适合自己的配置才是最好的配置，本项目在merlinclash、openclash、nikki、clashverge长时测试，merlinclash为主路由，openclash和nikki为旁路由，采用两个廉价机场长时验证，十分稳定，可实现长期免维护。

#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;仅提供基于Mihomo的配置文件示例，OpenClash、Nikki、Merlinclash等代理程序的设置可自行查阅相关教程，需一定科学网络配置基础才能上手。另外[HenryChiao/MIHOMO_YAMLS](https://github.com/gogyt/MIHOMO_YAMLS/tree/main/THEYAMLS/General_Config)项目收集了全网相对典型的yaml和ini订阅配置模板，可集思广益参考借鉴。

---
## 🚫 关于广告拦截
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 在代理程序中设置广告拦截仅仅是顺带功能，可设置简单的规则拦截，其他复杂拦截功能尽量不要放置在代理程序中，在终端安装例如AdGuard插件效果远远好于诸如OpenClash的广告拦截效果，还是遵循分工明确的原则，代理程序就主要干分流和代理的事。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 试用过[anti-AD](https://github.com/privacy-protection-tools/anti-AD)、[adblock](https://github.com/217heidai/adblockfilters)、[AWAvenue](https://github.com/TG-Twilight/AWAvenue-Ads-Rule)、[GEOSITE,category-ads-all](https://github.com/MetaCubeX/meta-rules-dat/blob/meta/geo/geosite/category-ads-all.list)等广告过滤列表，其中anti-AD、adblock是比较全面的广告列表，AWAvenue(秋风)、GEOSIET,category-ads-all是轻量化的广告列表，可相互搭配使用。adblock有近20万条拦截规则，拦截率可达惊人的50%以上(统计10万次连接，拦截数5万次以上)，anti-AD也有十多万条规则，拦截率也很高，但网评有误杀情况，当然，这跟个人上网习惯有关，推荐单独使用adblock，以及AWAvenue、category-ads-all搭配使用。还得看硬件的情况，硬件扛不住的，就用轻量化，或不用拦截规则，作者在华硕BE86U上测试，adblock能轻松运行，X86上就更没问题了。

---

-  ## ⚡ Mihomo通用yaml模板
#### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;配置模板适用于Mihomo内核的代理程序，如OpenClash、Nikki、Merlinclash、Clash Verge等，可直接导入模板使用或稍加改动即可。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 配置模板最多采用了五层策略架构，层次功能分明，故转层负责检测和确保地区节点可用，地区策略层负责节点选择的形式，节点选择方式有均衡、自动、smart、手动，所有故障转移均不直接选择最底层节点，而是地区策略组之间故障转移，如：故转-手动→全球手动→地区策略→均衡or自动（或smart）or手动→机场节点，“全球手动”可自定义选择喜欢的地区策略或单一节点，当"全球手动"的节点失联时，自动切换至可用节点，闲时几乎不产生代理流量，响应迅速，可实现长时免维护。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 规则数据来源主要是[MetaCubeX](https://github.com/MetaCubeX/meta-rules-dat/tree/meta/geo)规则数据库，MetaCubeX的规则一个是采用mihomo内置GEOSITE和GEOIP数据库，另一个是采用的MetaCubeX实时更新的GEO数据库，配置中内置了分区域节点的smart智能选择、自动选择、手动选择、故障转移、负载均衡等功能，仅需修改yaml文件中的机场地址和名称即可。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 各种配置大同小异，Pro和Plus类配置模板可实现指定机场分流出站，其余模板均是多机场节点混用出站。Plus采用多元故转默认地区节点，当首选地区策略全部节点断连时，自动切换至下一可用地区策略，实现更为稳定的网络体验。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;✔️ 系统上线后按自己需求选择好分流策略即可使用，控制面板中各个策略和节点连通性是否绿色的其实无关紧要，不用强迫症的不停点击测试连通性，系统会根据相关规则设定去判定节点的选择。

<div align="center">


| <div align="center">☑️</div> | <div align="center">🧮配置文件</div> | <div align="center">🥇推荐指数</div> | <div align="center">📈配置详情</div> | <div align="center">📑特点</div> |
| :--- | :--- | :--- | :--- | :--- |
| <div align="center">**1**</div> | 📄**Rule.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/Rule.yaml)</div> | 多机场混合出站 |
| <div align="center">**2**</div> | 📄**RulePro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/RulePro.yaml)</div> | 多机场**自定义**出站 |
| <div align="center">**3**</div> | 📄**RulePlus.yaml** | 🥇★★★★☆ | <div align="center">[跳转](yaml/RulePlus.yaml)</div> | 多机场**混合**或**自定义**出站，**多元**默认故转 **${\color{blue}\text{【推荐】}}$** |
| <div align="center">**4**</div> | 📄**RuleLite.yaml** | 🥉★★★ | <div align="center">[跳转](yaml/RuleLite.yaml)</div> | 极简分流，多机场混合出站
| <div align="center">**5**</div> | 📄**RuleLitePro.yaml** | 🥈★★★★ | <div align="center">[跳转](yaml/RuleLitePro.yaml)</div> | 极简分流，多机场**自定义**出站  **${\color{blue}\text{【推荐】}}$** |
| <div align="center">**6**</div> | 📄**RuleSmart.yaml** | 🥈★★★☆ | <div align="center">[跳转](yaml/RuleSmart)</div> | 适配Smart核心，多机场混合出站 |
</div>

---

-  ## ⚓ 特殊设置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在家庭网络中，常常有部分设备不需要科学代理，旁路由比较好设置，只需让需要代理设备的网关指向旁路由，不需代理的默认指向主路由即可；但也有设备仅少量代理需求，其余不走科学代理。特别是主路由比较特殊，既要少量代理，又要大部分直连，比如白群仅docker镜像库、Emby海报刮削需要科学代理，其余全部绕过内核走直连的情况（主要是群晖按普通规则代理后，可能会产生不必要的代理流量，实际上是不需要的），可以利用规则先后顺序正则匹配的特点来实现部分代理的要求，按先后顺序匹配指令，如果上位规则没有匹配上，则匹配下一项规则。根据这一特点，先将这类设备IP 与MAC地址绑定，再将不需代理的设备IP匹配走直连，其次让部分需要代理的设备IP 匹配Proxy规则，最后让部分需要代理的设备IP匹配走直连，将其放置在规则集的最前端即可。例如以下规则：

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
✨ **个人水平有限，难免有误，敬请谅解；如果配置对你有帮助，顺手点个 Star ！有更好的建议，欢迎Issues交流。**  
