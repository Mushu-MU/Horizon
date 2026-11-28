---
layout: default
title: "Horizon Summary: 2026-11-28 (ZH)"
date: 2026-11-28
lang: zh
---

> 从 46 条内容中筛选出 11 条重要资讯。

---

**科技新闻**
1. [Cacti 未修复零日：四个 HTTP 请求即可实现 RCE](#item-tech-news-1) ⭐️ 8.0/10
2. [Linux 内核 NFS 服务器曝 9.8 分预认证漏洞，攻击者可获 root](#item-tech-news-2) ⭐️ 8.0/10
3. [《我的世界》基岩版资源包漏洞影响 26.52 至 26.63，26.65 已修复](#item-tech-news-3) ⭐️ 8.0/10
4. [Google 提出 DeepCrossAttention，称同质量下最高 3 倍加速](#item-tech-news-4) ⭐️ 7.0/10
5. [Convex AI 编码 skill 被指未经披露上传应用创意](#item-tech-news-5) ⭐️ 7.0/10
6. [WeaveLotus：疑似越南关联黑客攻击东南亚军政机构](#item-tech-news-6) ⭐️ 7.0/10
7. [Q-Dir 与 DesktopOK 官方安装包被植入 Python 远控木马](#item-tech-news-7) ⭐️ 7.0/10
8. [瑞士：五起攻击中四起用 AI 智能体，两起攻破关键基础设施](#item-tech-news-8) ⭐️ 7.0/10
9. [微软将在 Windows Server 2028 中移除 WSUS 服务器角色](#item-tech-news-9) ⭐️ 7.0/10
10. [Drupal 警告又一严重漏洞遭利用，可致站点被接管](#item-tech-news-10) ⭐️ 7.0/10
11. [微软紧急热补丁修复 Windows Server 2025 崩溃](#item-tech-news-11) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Cacti 未修复零日：四个 HTTP 请求即可实现 RCE](https://thehackernews.com/2026/11/unpatched-cacti-zero-day-enables-rce-in.html) ⭐️ 8.0/10

安全研究人员公开了 Cacti Core 1.2.31（当前最新版本）的零日漏洞利用概念验证，命名为 4HTTP2SHELL 和 4HTTP2ROOT。该漏洞尚未分配 CVE 编号，也未见官方补丁，利用前提是站点启用了 guest 账户——从 Cacti 0.8.7 起该账户默认关闭。攻击者可在未登录、无有效 API 密钥的情况下，用四个 HTTP 请求从全新会话获得 Cacti 服务账户的命令执行权限。攻击链为：客账户通过 auth\_profile.php?action=update\_data 把非数字字符串写入 preview\_graphs\_per\_page 设置，形成二次 SQL 注入，在加载 graph\_view.php 时执行任意 SQL 修改 poller 表记录，最后由 graph\_realtime.php 读取该记录并传给 PHP popen\(\) 执行。

rss · The Hacker News · 11月27日 05:48

**「背景」** Cacti 是开源网络监控平台，其轮询器会按计划从被监控设备采集数据，配置等信息则保存在数据库中。Cacti 的 guest 账户提供无需登录的访客访问，但自 0.8.7 版起默认禁用；本次公开的利用链正是以该账户已被启用为前提。

**「影响与应对」** 受影响管理员应立即关闭 guest 账户并限制 Cacti Web 界面的访问范围，同时检查 poller 配置中是否出现异常命令值，待官方修复发布后尽快升级。由于 Cacti 常保存路由器、交换机、服务器等设备的凭据和连接信息，取得命令执行权限的攻击者可进一步横向渗透，或篡改 poller 表以压制告警。

**标签**: `#Cacti`, `#zero-day`, `#remote code execution`, `#open-source security`, `#vulnerability`

---

<a id="item-tech-news-2"></a>
### [Linux 内核 NFS 服务器曝 9.8 分预认证漏洞，攻击者可获 root](https://opensec.in/blog/nfs2root-cve-2026-99362) ⭐️ 8.0/10

OpenSec 披露 Linux 内核 NFS 服务器组件 nfsd 存在预认证堆溢出漏洞 CVE-2026-99362，CVSS 评分 9.8。攻击者无需登录，仅凭一条发往 tcp/2049 的连接即可越界写入内核堆并取得 root shell；该漏洞自 2014 年 Linux 3.16 起存在，影响启用 NFSv4.1 或 4.2 的文件服务器、NAS 与集群存储节点。修复已在 6.12.117、6.18.61、7.3.2 和 7.4-rc1 中发布，需升级内核并重启生效，无法立即升级的环境可用防火墙限制 tcp/2049 访问。CVE 于 2026 年 11 月 20 日公开，目前信息来自 OpenSec 的披露及聚合渠道转述，尚未见独立验证。

telegram · zaihuapd · 11月27日 12:57

**「背景」** nfsd 是 Linux 内核中的 NFS 服务器实现，客户端通过 tcp/2049 访问其导出的共享目录；NVD 记录的修复描述指出，问题出在 nfsd4\_sequence\(\) 在接受 slot seqid 之前收窄了回复缓冲区。Red Hat 同时说明，其默认配置并不运行或启用 nfsd，因此攻击面主要限于那些专门配置为导出 NFSv4.1 或 NFSv4.2 共享的系统。

**「受影响系统的处置选择」** 对开放 tcp/2049 的 NFS 服务器而言，处置只有两条路：升级到 6.12.117、6.18.61、7.3.2 或 7.4-rc1 等已修复内核并重启，或在无法立即升级时于防火墙阻断该端口的外部访问。由于该漏洞自 3.16 起就存在，仍运行旧发行版内核的设备（如 CentOS 7）需依赖厂商回移植的修复版本，不能仅凭上游主线版本号判断是否安全；直接将 NAS、文件服务器和集群存储节点的 2049 端口暴露在不可信网络中的部署风险最高。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://access.redhat.com/security/cve/cve-2026-99362">CVE-2026-99362 - Red Hat Customer Portal</a></li>
<li><a href="https://nvd.nist.gov/vuln/detail/cve-2026-99362">NVD-CVE-2026-99362</a></li>
<li><a href="https://app.opencve.io/cve/CVE-2026-99362">CVE-2026-99362 - Vulnerability Details - OpenCVE</a></li>
<li><a href="https://opensec.in/blog/nfs2root-cve-2026-99362">NFS2ROOT ( CVE - 2026 - 99362 ): pre-auth root in Linux nfsd | OpenSec</a></li>
<li><a href="https://www.getpagespeed.com/server-setup/security/nfs2root-cve-2026-99362-centos-7">NFS2ROOT ( CVE - 2026 - 99362 ) on CentOS 7: Fixed Kernel</a></li>

</ul>
</details>

**标签**: `#Linux kernel`, `#NFS`, `#security vulnerability`, `#remote exploit`, `#CVE-2026-99362`

---

<a id="item-tech-news-3"></a>
### [《我的世界》基岩版资源包漏洞影响 26.52 至 26.63，26.65 已修复](https://www.zaikei.co.jp/article/20261119/878386.html) ⭐️ 8.0/10

附加组件开发者 8Crafter 于 11 月 15 日在 Reddit 公开称，《我的世界》基岩版资源包若包含 content.zipe 文件，可篡改游戏界面框架 Ore UI 并运行隐藏脚本，已确认影响 26.52 至 26.63 版本，覆盖 PC、手机和主机，Java 版不受影响。加入服务器或 Realm 且开启资源包自动下载时，玩家可能在未手动安装的情况下收到问题文件；已报告的利用后果包括删除全部存档、获取玩家 IP，以及在 Windows 特定条件下无提示打开任意 URI 或启动资源包内的批处理文件下载恶意软件。Mojang 已在 26.65 版修复。AxmBro 发布的 Windows 只读检测工具能查找 content.zipe，但不能判定资源包是否恶意。

telegram · zaihuapd · 11月27日 18:04

**「背景」** 资源包通常用于替换材质、界面等游戏内容，基岩版服务器和 Realm 可让客户端自动下载资源包以同步体验。此次问题在于资源包能够触及 Ore UI 并执行隐藏脚本，而不只是改变外观。

**「影响与应对」** 对服务器和 Realm 运营者而言，在升级到 26.65 前应关闭资源包自动下载或限制资源包来源，玩家则应避免加载来源不明的资源包；检测工具只能作为排查线索，不能替代升级和人工审查。

**标签**: `#Minecraft Bedrock`, `#security vulnerability`, `#resource packs`, `#malware`, `#game security`

---

<a id="item-tech-news-4"></a>
### [Google 提出 DeepCrossAttention，称同质量下最高 3 倍加速](https://research.google/blog/supercharging-transformer-residual-connections/) ⭐️ 7.0/10

Google Research 在一篇博客中介绍 DeepCrossAttention，这是一种改造 Transformer 残差连接的方法，研究团队声称在模型质量相当的情况下可实现最高 3 倍加速。当前材料没有给出具体模型规模、基准测试、硬件配置或可复现实验细节，因此这一 3 倍应视为研究团队声明，而非独立复现结果。对关注训练或推理效率的读者，关键待确认点是加速适用于哪个阶段，以及能否与现有 Transformer 实现兼容。

hackernews · ComputedCamp995 · 11月27日 23:06 · [社区讨论](https://news.ycombinator.com/item?id=50672565)

**「背景」** Transformer 的残差连接通常把前面各层输出直接相加，而 Google 的研究指出这种做法可能稀释关键信息；DeepCrossAttention 改用带可学习权重的跨层注意力路由，不再只做简单的顺序相加。该方法并非首次亮相：相关论文已以《DeepCrossAttention: Supercharging Transformer Residual Connections》为题发表于 ICML 2025，本次 Google Research 博客是对该工作的进一步介绍。

**「影响」** 在可复现基准和实现细节公布前，使用 Transformer 的团队不应把最高 3 倍加速纳入容量规划；现有证据也不足以判断替换残差连接会如何影响训练或推理栈的兼容性与吞吐。

**「社区讨论」** Hacker News 评论没有提供复现或性能反证；有评论批评原文用折线图连接不同方法缺乏时间关系，另一条评论则把该思路类比为 DenseNet。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://research.google/blog/supercharging-transformer-residual-connections/">Supercharging transformer residual connections</a></li>
<li><a href="https://arxiv.org/html/2502.06785">DeepCrossAttention : Supercharging Transformer Residual ...</a></li>
<li><a href="https://scholar.google.com/citations?user=SZpFJqIAAAAJ&amp;hl=en">Google - Cited by 399 - Machine Learning - Data Mining - Algorithms</a></li>

</ul>
</details>

**标签**: `#transformers`, `#model efficiency`, `#attention mechanisms`, `#Google Research`, `#deep learning`

---

<a id="item-tech-news-5"></a>
### [Convex AI 编码 skill 被指未经披露上传应用创意](https://github.com/convex/convex-backend-skill/issues/64) ⭐️ 7.0/10

GitHub 上一个 issue 指控 Convex 的 AI 编码“skill”在未告知用户的情况下，将用户的应用创意发送到远程服务器。Convex CEO Jamie 在评论中回应称，该插件中的 prompt 上传用于支撑 Convex 的“quickstart”功能，是最近关闭的端到端 vibe-coding 产品 Convex Chef 的延续。目前可见材料只有 issue 片段和评论摘录，尚无独立验证或完整技术细节，因此上传范围、披露方式与是否获得同意仍不清楚。

hackernews · MickyTheMouse · 11月27日 18:02 · [社区讨论](https://news.ycombinator.com/item?id=50669765)

**「背景」** 这里所说的“skill”是供 AI 编程代理调用的可复用指令或工具包，Convex 的插件通过它提供快速上手（quickstart）流程。Convex CEO 在评论中称，该流程是最近关闭的端到端“vibe-coding”产品 Convex Chef 的延续。

**「影响」** 对使用该 skill 的开发者而言，直接后果是他们无法仅凭插件界面判断应用创意是否离开本机；在 Convex 说明具体上传字段、触发时机和保留策略前，涉及未公开产品创意的团队应审计网络请求或避免输入敏感内容。

**「社区讨论」** 评论者 jaynate 认为，相比模型自行发起恶意工具调用，prompt injection 更常见，并明确表示这不等于本次事件出于恶意；quantum\_state 则主张，长期看自托管开放权重模型是更可靠的方向。

**标签**: `#privacy`, `#ai-coding-tools`, `#developer-tools`, `#data-handling`, `#open-source`

---

<a id="item-tech-news-6"></a>
### [WeaveLotus：疑似越南关联黑客攻击东南亚军政机构](https://thehackernews.com/2026/11/suspected-vietnam-linked-hackers-target.html) ⭐️ 7.0/10

SOCRadar 披露了一个此前未记录的疑似越南关联网络间谍活动集群 WeaveLotus，并将其归为 RedOps 行动：2026 年 8 月至 9 月，攻击者针对菲律宾、泰国和印度尼西亚的政府、军事与立法机构进行侦察，并在泰国和菲律宾确认了五起入侵。攻击者主要利用 GeoServer（CVE-2024-36401）、JasperReports 默认管理员口令、osTicket（CVE-2021-42235）SQL 注入和暴露的 Laravel 调试模式获取初始访问，再通过反向 SSH 隧道维持内网访问并横向移动。SOCRadar 称，判断与越南有关联的依据包括越南语代码注释、UTC+07:00 作业时间和区域战略目标，但现有证据支持将其作为独立活动集群跟踪，尚不能最终确认国家赞助。

rss · The Hacker News · 11月27日 16:36

**「背景」** GeoServer、JasperReports、osTicket 和 Laravel 都是常见的开源 Web 应用或框架；一旦它们暴露在互联网上，并且保留默认口令、调试模式或未修补漏洞，攻击者就可能直接获得服务器或数据库访问权限。反向 SSH 隧道则允许位于内网的受控主机主动连接外部基础设施，从而绕过仅限制入站连接的边界防护。

**「影响」** 对运行上述系统的东南亚政府、军事和立法机构而言，最直接的处置是修补 GeoServer CVE-2024-36401 与 osTicket CVE-2021-42235、更换 JasperReports 默认 jasperadmin 口令、关闭 Laravel 调试模式，并排查异常的 443 端口 SSH 出站连接及相关账号活动。

**标签**: `#cybersecurity`, `#nation-state threats`, `#vulnerability exploitation`, `#open-source software`, `#Southeast Asia`

---

<a id="item-tech-news-7"></a>
### [Q-Dir 与 DesktopOK 官方安装包被植入 Python 远控木马](https://thehackernews.com/2026/11/hackers-trojanize-official-q-dir-and.html) ⭐️ 7.0/10

安全公司 AhnLab 披露，SoftwareOK 官网分发的 Q-Dir 与 DesktopOK 安装文件及更新流程均遭篡改，会在运行正常程序的同时从外部服务器下载并部署 Python 远控木马。被确认植入恶意代码的版本包括 Q-Dir 12.85.0.0、12.84.0.0、12.83.0.0，以及 DesktopOK 12.85.0.0、12.82.0.0；攻击者如何替换官方安装包尚不清楚。恶意安装器会从 mail.c1a2\[.\]top 获取 7zr.exe 和包含 RAT 与 Python 运行时的 dsv2\_py39\_agent.7z，并通过伪装成 Microsoft Edge 的计划任务执行 py\_client\_dsv2.py，连接 8.210.69\[.\]51:9876 后支持命令与 Python 代码执行、文件传输、截屏和系统信息收集，还会枚举本机安全软件。AhnLab 建议用户校验文件哈希并排查异常 Python 环境、计划任务和外部通信，因为仅卸载重装可能无法清除已安装的 RAT；目前未归因任何已知攻击组织，但恶意代码中含中文注释。

rss · The Hacker News · 11月27日 09:29

**「背景」** Q-Dir 是 SoftwareOK 开发的免费轻量级 Windows 文件管理器，DesktopOK 则用于保存和恢复桌面图标位置；两者通常都从同一官方站点下载或更新。此次事件的关键在于，攻击者篡改的是用户原本信任的官方分发和更新链路，而非仿冒域名或第三方打包站点，因此仅凭“从官网下载”并不足以判断文件安全。

**「受影响用户」** 对使用受影响版本的用户和组织来说，卸载并重装 Q-Dir 或 DesktopOK 不足以清除风险，因为 AhnLab 指出已植入的 Python RAT 可能不会被移除。应按其建议校验安装包 SHA-256，检查伪装成 Microsoft Edge 的计划任务、py\_client\_dsv2.py、异常 Python 运行环境以及与 mail.c1a2\[.\]top 和 8.210.69\[.\]51:9876 的网络通信，再更新杀毒引擎并全盘扫描。

**标签**: `#cybersecurity`, `#supply-chain-attack`, `#malware`, `#windows`, `#software-updates`

---

<a id="item-tech-news-8"></a>
### [瑞士：五起攻击中四起用 AI 智能体，两起攻破关键基础设施](https://thehackernews.com/2026/11/switzerland-confirms-ai-assisted.html) ⭐️ 7.0/10

瑞士国家网络安全中心（NCSC）表示，在五起已确认的针对瑞士组织的攻击中，有四起使用了 AI 智能体，这是该国首次出现此类案例；其中三起针对关键基础设施运营商，两起成功入侵，但未报告重大中断。NCSC 主任 Florian Schütz 在瑞士公共广播 SRF 的采访中给出上述数字，并称五起案件均在近日上报，受害者包括中小企业，但受害者和攻击者身份均未公布。该中心周二发布的安全公告称，在当时已知的每起案件中，AI 智能体都侵入了受害者的 IT 系统；公告和采访均未解释案件统计为何发生变化。NCSC 将这些工具称为“智能体化攻击框架”，仅把 ARTEX 和 CyberStrikeAI 列为互联网上可获取的示例，并未认定它们用于这五起案件。

rss · The Hacker News · 11月27日 06:04

**「何为“智能体攻击框架”」** 瑞士联邦网络安全局所说的“智能体攻击框架”（agentic offensive framework），是指由 AI 推理模型端到端驱动的攻击工具：它们把渗透测试能力与自主推理结合，自行寻找漏洞、发起利用，并根据防守反应在数秒内切换手法。Elastic Security Labs 的分析指出，这类框架与传统 C2 框架的关键差别在于攻击效果以秒计落地，且可并行发起多路尝试。Spectrum Security 的统计显示，ARTEX、CyberStrikeAI、PentAGI、Cairn 等框架已有 2335 个暴露在互联网上的控制台，并识别出 47 个 ARTEX 变体和三款此前未被记录的智能体攻击工具，说明这类工具在此次瑞士通报之前就已在真实入侵中被使用。

**「影响」** 对关键基础设施运营商和中小企业而言，直接后果是攻击者可并行扫描未修补漏洞，并在防御响应时迅速切换手法，压缩检测和响应时间；NCSC 建议面向互联网的系统在关键更新发布后 24 小时内打补丁，隔离无法快速修补的系统，并对互联网可达服务启用多因素认证（MFA）或通行密钥（passkey）、最小权限和异常流量监控。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://ai-threat.watch/aof/artex/">ARTEX : agentic offensive framework | AI Threat Watch</a></li>
<li><a href="https://www.elastic.co/security-labs/threat-command/agentic-offensive-frameworks-detection-artex">Inside the loop: Five AI attack frameworks that never ask permission</a></li>

</ul>
</details>

**标签**: `#AI-assisted cyberattacks`, `#critical infrastructure security`, `#cybersecurity`, `#AI agents`, `#Switzerland`

---

<a id="item-tech-news-9"></a>
### [微软将在 Windows Server 2028 中移除 WSUS 服务器角色](https://www.bleepingcomputer.com/news/microsoft/microsoft-removes-wsus-server-role-in-windows-server-2028/) ⭐️ 7.0/10

微软计划在下一代主要版本 Windows Server 2028 中移除 WSUS 服务器角色。这项调整影响负责企业 Windows 补丁管理的 IT 管理员，意味着继续依赖 WSUS 服务器角色的现有流程需要调整；现有报道仅给出简短通知，未说明迁移步骤或替代方案。

rss · BleepingComputer · 11月27日 11:18

**「背景：WSUS 是什么」** WSUS（Windows Server Update Services）是微软面向企业内网的补丁分发工具，管理员可通过它集中审批并下发 Windows 更新；据 comss.ru 报道，该功能于 2005 年以 Software Update Services（SUS）之名推出。Windows Server 2028 是微软服务器操作系统的下一个大版本，此次被移除的是其中的 WSUS 服务器角色。

**「影响」** 仍依赖 WSUS 进行内网补丁集中审批和分发的企业，需要在升级到 Windows Server 2028 前将补丁管理流程迁移到其他机制；由于现有来源只确认该角色被移除、未提供迁移路径，受影响的 IT 团队需自行评估替代方案并预留测试时间。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.comss.ru/page.php?id=23115">Microsoft удалит роль WSUS из Windows Server 2028</a></li>
<li><a href="https://inventivehq.com/blog/windows-update-commands-powershell-usoclient-amp-wuauclt">Windows Update Commands: Force Updates via USOClient (2026)</a></li>

</ul>
</details>

**标签**: `#WSUS`, `#Windows Server`, `#Microsoft`, `#patch management`, `#enterprise IT`

---

<a id="item-tech-news-10"></a>
### [Drupal 警告又一严重漏洞遭利用，可致站点被接管](https://www.bleepingcomputer.com/news/security/drupal-warns-of-new-access-bypass-flaw-exploited-in-attacks/) ⭐️ 7.0/10

Drupal 安全团队警告称，攻击者正在利用第二个严重漏洞入侵并接管未打补丁的网站。该漏洞被描述为访问绕过类问题，但当前信息未提供受影响版本、CVE 编号或具体修复与缓解措施。运行 Drupal 的站点运营者需留意官方后续公告，并在补丁或处置指引发布后尽快处理。

rss · BleepingComputer · 11月27日 10:10

**「背景」** 在这一警告之前，Drupal 核心于 2026 年 11 月 18 日发布了高危远程代码执行公告 SA-CORE-2026-017，指出攻击者可通过 install.php 在特定条件下尝试重装 Drupal，从而导致站点接管或远程代码执行；该公告还称，最早在 2026 年 11 月 19 日 19:00 UTC 已观察到线上站点被利用。Drupal 的安全公告页面同时说明，相关漏洞目前被评为 critical，至少有一个可被匿名用户利用，且不止一种配置会受影响。

**「影响与应对」** 根据 SA-CORE-2026-019，暴露面集中在处于异常或未完成安装状态的 Drupal 站点（包括生产站点）：这类站点即使已经应用了修复安装程序漏洞的 SA-CORE-2026-017，仍可能被攻击者接管。运维方应移除或妥善保护 core 自带的 install.php 安装程序并应用 2026-019 的修复；已加固安装程序的站点不受该问题影响。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.drupal.org/security">Security advisories | Drupal.org</a></li>
<li><a href="https://www.drupal.org/sa-core-2026-017">Drupal core - Highly critical - Remote code execution - SA ...</a></li>
<li><a href="https://www.drupal.org/sa-core-2026-019">Highly critical - Access bypass - SA-CORE-2026-019 - Drupal</a></li>

</ul>
</details>

**标签**: `#Drupal`, `#security vulnerability`, `#active exploitation`, `#web security`, `#open source CMS`

---

<a id="item-tech-news-11"></a>
### [微软紧急热补丁修复 Windows Server 2025 崩溃](https://www.bleepingcomputer.com/news/microsoft/new-out-of-band-oob-emergency-hotpatch-fixes-windows-server-2025-crashes/) ⭐️ 7.0/10

微软已发布紧急热补丁，修复 Windows Server 2025 在安装本月安全热补丁 KB5131077 后出现的崩溃问题。该修复针对已经安装 KB5131077 并受影响的服务器，属于紧急更新而非例行补丁。

rss · BleepingComputer · 11月27日 09:08

**「背景」** 微软于 2026 年 11 月 10 日发布安全热补丁 KB5131077（OS Build 26100.33730），并在说明中称已将 Windows Server 2025 的最新服务堆栈更新 KB5131079（26100.33822）与热补丁合并，以提升更新过程可靠性。此次紧急带外修复以 KB5138318 发布，将系统版本提升到 26100.33732，针对的正是 KB5131077 引入的 IPv6 相关崩溃问题。

**「影响」** 已安装 KB5131077 的 Windows Server 2025 管理员需要评估并部署该紧急热补丁，以消除崩溃问题；来源未披露受影响的具体版本范围、回滚步骤或是否必须重启。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.bleepingcomputer.com/news/microsoft/new-out-of-band-oob-emergency-hotpatch-fixes-windows-server-2025-crashes/">Microsoft pushes emergency hotpatch to fix Windows Server crashes</a></li>
<li><a href="https://support.microsoft.com/en-us/servicing/os/hotpatch/windows-server-2025/2026/november-kb5131077-windows-server-2025-hotpatch-update">November 10, 2026—Hotpatch KB5131077 (OS Build 26100.33730)</a></li>
<li><a href="https://windowsreport.com/windows-server-2025-kb5138318-oob-hotpatch-fixes-ipv6-related-crash-bug-caused-by-kb5131077/">Windows Server 2025 KB5138318 OOB hotpatch ... - Windows Report</a></li>

</ul>
</details>

**标签**: `#Windows Server`, `#Microsoft`, `#emergency patch`, `#reliability`, `#system administration`

---