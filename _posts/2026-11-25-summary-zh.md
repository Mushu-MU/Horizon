---
layout: default
title: "Horizon Summary: 2026-11-25 (ZH)"
date: 2026-11-25
lang: zh
---

> 从 48 条内容中筛选出 11 条重要资讯。

---

**科技新闻**
1. [Check Point 安全管理服务器遭入侵，攻击者伪造会话](#item-tech-news-1) ⭐️ 8.0/10
2. [Simon Willison 回顾 LLM 与编程代理的三个拐点](#item-tech-news-2) ⭐️ 8.0/10
3. [VMware vCenter 修复 9.8 分鉴权绕过等 23 个漏洞](#item-tech-news-3) ⭐️ 8.0/10
4. [单比特 .NET 改动绕过 Windows 代码完整性与 VirtualBox 加固](#item-tech-news-4) ⭐️ 8.0/10
5. [微软修复 Azure API Management Classic 漏洞](#item-tech-news-5) ⭐️ 8.0/10
6. [Ternary Bonsai 2.5 27B 社区实测：22–25 tok/s 与 128k 上下文](#item-tech-news-6) ⭐️ 7.0/10
7. [WHMCS 未认证 SQL 注入可泄露客户数据与管理员哈希](#item-tech-news-7) ⭐️ 7.0/10
8. [OpenAI 与 Cisco 发布 Shirudo：AI 生成 eBPF 补丁前防护](#item-tech-news-8) ⭐️ 7.0/10
9. [CISA 将 MailAssure 与 MONAI Label 漏洞列入 KEV](#item-tech-news-9) ⭐️ 7.0/10
10. [Rackspace 因安全泄露关停 Spot 云平台](#item-tech-news-10) ⭐️ 7.0/10
11. [开发者指控 T3 Code 默认遥测并上传凭证哈希](#item-tech-news-11) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Check Point 安全管理服务器遭入侵，攻击者伪造会话](https://www.greynoise.io/blog/check-point-security-management-servers-intrusion-campaign) ⭐️ 8.0/10

GreyNoise 报告称，一场仍在进行的入侵活动利用多个漏洞攻破了 22 个组织中的 24 台 Check Point 安全管理服务器。分析重点描述的一种手法是：攻击者反复请求 HFS 登录接口，收集 JavaScript Math.random\(\) 的输出，重建 Node.js V8 PRNG 的内部状态，从而恢复会话 Cookie 签名密钥并伪造管理员会话 Cookie。

hackernews · louiereederson · 11月24日 16:32 · [社区讨论](https://news.ycombinator.com/item?id=50630594)

**「背景」** Check Point 曾为 Security Management Server 与多域安全管理服务器（MDS）中的认证绕过漏洞分配 CVE-2026-16232，并于 7 月 22 日发布 Jumbo Hotfix；该漏洞可让未认证攻击者取得应用登录令牌，并以完整权限进入 SmartConsole。GreyNoise 称本轮攻击活动发生在 2026 年 10 月 17 日至 11 月 2 日，至少波及 22 个组织。

**「受影响范围与处置重点」** 对仍自行托管 Check Point 安全管理服务器的组织来说，需要处置的是 R81.10、R81.20、R82、R82.10 以及更早版本上的 CVE-2026-16232，以及同一批次披露的 CVE-2026-62144 和 CVE-2026-62145；Check Point 表示 Smart-1 Cloud 客户已受保护，因此这些客户不必按同样范围自查。由于此次攻击针对的是管理服务器本身，在完成升级前，将 SmartConsole 等管理接口从公网收回，是现有证据下最直接的缓解动作。

**「社区讨论」** 评论对初始访问路径提出疑问，并追问这些组织的 Check Point 安全管理服务器是否都暴露在互联网上。另有评论认为，与其逐一修复误用 Math.random\(\) 的应用，不如让随机数生成器默认具备安全性。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.greynoise.io/blog/check-point-security-management-servers-intrusion-campaign">An Active Intrusion Campaign Against Check Point Security ...</a></li>
<li><a href="https://support.checkpoint.com/results/sk/sk185169/">sk185169 - CVE - 2026 - 16232 - Authentication bypass with...</a></li>
<li><a href="https://www.linkedin.com/posts/mathewvincent_check-point-fixes-actively-exploited-authentication-activity-7486638914766716930-VggP">Check Point fixes actively exploited authentication bypass...</a></li>
<li><a href="https://www.rapid7.com/blog/post/etr-cve-2026-16232-critical-check-point-smartconsole-authentication-bypass-exploited-in-the-wild/">CVE - 2026 - 16232 : Critical Check Point SmartConsole Authentication...</a></li>
<li><a href="https://github.com/advisories/ghsa-m2xx-23gx-734v">An authentication bypass vulnerability in the Check Point ...</a></li>

</ul>
</details>

**标签**: `#security`, `#intrusion campaign`, `#PRNG`, `#Check Point`, `#exploitation`

---

<a id="item-tech-news-2"></a>
### [Simon Willison 回顾 LLM 与编程代理的三个拐点](https://simonwillison.net/2026/Nov/24/llm-inflection-points/) ⭐️ 8.0/10

在这篇 2026 年 11 月 24 日发布的回顾文章中，Simon Willison 提出过去十二个月 LLM 与编程代理出现了三个能力拐点：2025 年 11 月的 Claude Opus 4.5 以及同月的 OpenAI GPT-5.1 和 Codex 系列，让编程代理首次在他的日常任务中稳定可用；2026 年 6 至 7 月的 Claude Fable 5 等“Fable 类”模型，能在给定目标和工具后自行解决复杂问题；2026 年 9 至 10 月的 Opus 5.5 等模型则在 3D 建模和游戏开发上明显进步，甚至能按“更有趣”的指令重新平衡玩法。Willison 称这些能力已成为他对前沿模型的基线预期，并用自己修复 Safari 显示问题、定位神秘蜂鸣声和制作 RTS 游戏的经历举例。文章是作者基于个人使用体验的回顾性分析，不是新模型发布或独立基准测试。

rss · Simon Willison · 11月24日 23:02

**「背景」** 这篇回顾以 Claude Opus 4.5 发布一周年为时间锚点；Claude Code 早在 2025 年 2 月 24 日随 Claude 3.7 Sonnet 推出，到 Opus 4.5 面世时已运行约九个月。据当时报道，Fable 5 在 2026 年 6 月发布后很快被美国出口管制禁止，6 月 30 日管制解除后于 7 月 1 日恢复上线，并加入了新的网络安全分类器。

**「对独立游戏开发者的直接影响」** 对独立游戏开发者而言，具体变化是可玩性调优进入了“可提示迭代”的范围：Willison 记录 Opus 5.5 用 12 小时自行试玩并重新平衡数值，把一个原本无聊的即时战略游戏改到“好玩”。随之而来的是披露压力——独立游戏圈已因 AI 辅助编程陷入争议，而 Take-Two 方面称 GTA 6 中生成式 AI 的参与度为“零”，并将其描述为最后一部“前 AI 时代”大作，这条界线正在成为发行与评奖环节的现实考量。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://app.stationx.net/articles/sec-ai-news-i-asked-my-ai-to-design-its-own-body">Sec &amp; AI News — I Asked My AI to Design Its Own Body ( 2026 )</a></li>
<li><a href="https://www.gamesradar.com/games/grand-theft-auto/ahead-of-gta-6-take-two-ceo-calls-out-anthropic-and-openai-over-ai-game-clones-as-its-ironic-to-stomp-on-someone-elses-ip/">Ahead of GTA 6 , Take - Two CEO calls out Anthropic... | GamesRadar+</a></li>
<li><a href="https://thenextweb-com.nproxy.org/news/take-two-gta6-no-generative-ai-handcrafted">GTA 6 uses zero generative AI , Take - Two CEO Strauss Zelnick...</a></li>

</ul>
</details>

**标签**: `#LLM coding agents`, `#AI engineering`, `#Claude Opus 4.5`, `#industry analysis`

---

<a id="item-tech-news-3"></a>
### [VMware vCenter 修复 9.8 分鉴权绕过等 23 个漏洞](https://thehackernews.com/2026/11/vmware-vcenter-hit-by-another-critical.html) ⭐️ 8.0/10

Broadcom 为 VMware ESX、vCenter、Workstation、Fusion 和 Avi Load Balancer 发布 23 个漏洞的补丁，其中 vCenter 的 CVE-2026-123903 位于 VMware Directory Service（vmdir），CVSS 评分为 9.8，网络可达 vCenter 的攻击者可绕过认证并获得未授权访问。vCenter 另有 CVE-2026-123904（CVSS 7.5，处理特定压缩包时可任意写文件并可能导致代码执行）及三个 7.5 分的目录服务拒绝服务漏洞（CVE-2026-123905 至 CVE-2026-123907）一并修复。受影响部署应在 vCenter 8.0 U3m、9.1.2、9.0.2.0300 或 Cloud Foundation 5.2.5 等对应版本中修复；vCenter 7.0 处于扩展支持的用户需联系 Broadcom 支持。Broadcom 未说明这些新漏洞已被在野利用，但几天前另一枚同样 9.8 分的 vmdir 鉴权绕过 CVE-2026-123890 曾被作为零日利用，VMware 称两者是不同且无关的问题。

rss · The Hacker News · 11月24日 13:28

**「背景：vmdir 与上一枚 9.8 分漏洞」** VMware Directory Service（vmdir）是 vCenter 内置的目录服务，承担身份认证等核心功能，因此该组件中的鉴权绕过一旦可被网络访问利用，影响面直接覆盖整个 vCenter 管理面。就在几天前，Broadcom 刚修补了同一组件中的另一个 9.8 分鉴权绕过漏洞 CVE-2026-123890，该漏洞曾被疑似具有中国背景的 Armory Castle 组织作为零日利用；VMware 表示新披露的 CVE-2026-123903 是独立问题，与前者无关。

**「影响与处置」** 只要 vCenter 管理接口可被攻击者从网络访问，该 9.8 分漏洞就构成直接的认证绕过风险，运维方应按所用产品版本升级到对应的修复版本。Cloud Foundation、Telco Cloud Platform 和 Telco Cloud Infrastructure 的修复也依赖 vCenter 8.0 U3m，而 vCenter 7.0 扩展支持用户没有列出的独立补丁版本，需要联系 Broadcom 支持确认升级路径。

**标签**: `#VMware vCenter`, `#authentication bypass`, `#critical vulnerability`, `#security patching`, `#CVE-2026-123903`

---

<a id="item-tech-news-4"></a>
### [单比特 .NET 改动绕过 Windows 代码完整性与 VirtualBox 加固](https://thehackernews.com/2026/11/google-researcher-shows-how-single-bit.html) ⭐️ 8.0/10

Google Project Zero 研究员 James Forshaw 演示，.NET Framework 4 在程序文件无法作为映像加载时会回退为从内存加载；清除 .NET 文件头中的 IMAGE\_FILE\_EXECUTABLE\_IMAGE 标志位即可让映像加载调用拒绝该文件，而 .NET 仍会加载并运行它，从而在 Windows 11 S 模式下绕过用户模式代码完整性（UMCI）。同一加载路径还绕过了 Oracle VirtualBox 的 Windows 主机进程加固：VirtualBox 对 AnyCPU .NET 文件返回触发回退的错误，文件因此从加固未检查的路径进入受保护的 VirtualBox 进程；该问题为 CVE-2026-87268（Oracle 评分 7.8，列出 VirtualBox 7.2.16 受影响），Windows 代码完整性问题为 CVE-2026-108398（Microsoft 评分 8.8，属本地低权限安全功能绕过）。Oracle 在 9 月修复 VirtualBox 问题（表格将 7.2.18 列为修复构建，但正文又称 7.2.16 和 7.2.18 受影响，应核对实际运行版本），Microsoft 于 10 月 13 日发布按 Windows 和 .NET Framework 版本区分的更新。利用条件有限：VirtualBox 场景要求攻击者已是主机普通用户，代码运行在受保护的 VirtualBox 进程内而非从客户机逃逸到主机；.NET 场景需要一个愿意加载程序集的程序，不能仅凭网络接管任意 Windows 机器；Forshaw 还通过 COM 劫持将测试代码送入 PPL 进程，该路径没有单独 CVE，且 10 月修复未改变受保护进程的加载行为，研究人员认为它仍可能有效。

rss · The Hacker News · 11月24日 12:02

**「背景」** .NET Framework 4 在按可执行映像加载程序文件失败并遇到特定错误时，会退回到将该文件作为普通内存副本加载；这条回退路径不会执行已加载映像所面对的检查。Windows 的 UMCI 和 VirtualBox 的进程加固都依赖映像加载路径来限制或监控代码，因此 .NET 的加载回退成为绕过这些保护的关键前提。

**「影响与处置」** 对受影响组织而言，补丁核对比版本号假设更重要：VirtualBox 需确认运行构建包含 Oracle 9 月修复（源文对 7.2.18 的受影响状态表述不一），Windows 需安装与具体 Windows 和 .NET Framework 版本匹配的 10 月 13 日更新，例如 Windows 11 26H2 对应 KB5127694，而不是套用单一通用包。研究人员还提醒，10 月修复只纠正 UMCI 策略检查，未改变受保护进程的加载行为，因此通过 PPL 的利用路径没有单独 CVE，且可能仍然有效。

**标签**: `#security research`, `#Windows`, `#.NET`, `#code integrity`, `#VirtualBox`

---

<a id="item-tech-news-5"></a>
### [微软修复 Azure API Management Classic 漏洞](https://thehackernews.com/2026/11/microsoft-fixes-azure-api-management.html) ⭐️ 8.0/10

微软于 2026 年 11 月 18 日发现、19 日关闭了 Azure API Management Classic 层级的一条未授权访问路径；在服务未按安全最佳实践配置时，该问题可能允许访问管理功能，并暴露 Named Values、身份提供商和 OpenID Connect 的客户端密钥、订阅密钥以及直连管理 API 令牌，v2 层级不受影响。挪威国家安全局（NSM）表示，一个未知行为者一直在 APIM 中搜寻访问令牌、密钥和命名值，波及挪威多家企业，包括能源公司 Equinor 和 Skagerak Energi，但尚未发现对挪威企业造成实际影响。微软于 11 月 21 日发布指引，帮助客户识别并轮换相关凭据，未披露受影响客户数量，并称在发现问题前未授权方可能已访问 Classic 实例中存储的密钥。

rss · The Hacker News · 11月24日 10:44

**「背景」** Azure API Management 是微软用于发布、管理和保护 API 的云服务，此次受影响的是其中的 Classic 层级，v2 层级不受影响。Named Values 是该服务中用于保存配置值的机制，可存放客户端密钥、订阅密钥等敏感凭据，因此一旦该层级的管理功能被非授权访问，攻击者寻找这些值就直接关系到下游服务的凭据安全。

**「客户需轮换 APIM 凭据」** 对使用 Azure API Management Classic 层的客户而言，最直接的后果是必须排查并轮换实例中配置的密钥：可能被未授权方访问的包括命名值（Named Values）中的密钥、身份提供方与 OpenID Connect 提供方的客户端密钥、订阅密钥，以及调用直接管理 API 所用的令牌。微软已于 2026 年 11 月 21 日发布相关指引；由于这类凭据可直接用于访问其保护的后端服务，实际能触及的范围取决于该凭据的权限以及它是否仍然有效，因此在完成轮换前应按已泄露处理。

**标签**: `#Azure API Management`, `#cloud security`, `#vulnerability`, `#active exploitation`, `#secrets management`

---

<a id="item-tech-news-6"></a>
### [Ternary Bonsai 2.5 27B 社区实测：22–25 tok/s 与 128k 上下文](https://prismml.com/news/bonsai-2-5-27b) ⭐️ 7.0/10

Ternary Bonsai 2.5 27B 发布后，社区测试显示其 Q2 GGUF 版本在 24GB 内存的 Mac Mini M5 Pro 上生成速度约为 22–25 token/s，并能较轻松地容纳 128k 上下文。有人用自建长任务基准对比，Bonsai 2.5 与 Bonsai2 均为 8 项通过 5 项，但步骤减少 17%、耗时从 107 分钟降至 76 分钟；同一测试中 Opus 5.5 为 8/8。另有评论者称该模型在 SWE-bench Verified 上与 Opus 4.6 相当，但没有给出具体分数，并提醒该基准代表性有限，相关结论仍需独立验证。

hackernews · b0m · 11月24日 20:08 · [社区讨论](https://news.ycombinator.com/item?id=50633922)

**「背景」** Ternary（三进制）以 3 为基数，平衡三进制用 −1、0、+1 三个取值来表示数值。Bonsai 2.5 27B 标题中的“Ternary”指向三值量化路线：把模型权重压到三种状态，以降低本地推理的存储与内存开销。

**「影响」** 对想在单机或小型设备上运行长上下文编码代理的开发者，报告中 24GB 内存配置可较轻松承载 128k 上下文，使批处理式代理任务值得实测；但速度、通过率和基准分数都来自零散社区测试，部署前应在自己的硬件和量化格式上复测。

**「社区讨论」** 评论者既惊叹小模型的进步，也要求更可比的数据：有人要求给出与 Qwen3.8 的 Q1/Q2 量化版或 1B–10B 级模型的直接对比，并怀疑 SWE-bench Verified 的结果可能受针对基准优化或基准漂移影响。自建长任务测试则显示 Bonsai 2.5 比上一版更快、步骤更少，但通过数没有提高，仍明显落后于 Opus 5.5 的 8/8。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Ternary_numeral_system">Ternary numeral system - Wikipedia</a></li>

</ul>
</details>

**标签**: `#ternary-quantization`, `#local-llm-inference`, `#model-release`, `#agentic-coding`, `#llm-benchmarks`

---

<a id="item-tech-news-7"></a>
### [WHMCS 未认证 SQL 注入可泄露客户数据与管理员哈希](https://thehackernews.com/2026/11/whmcs-sql-injection-flaw-could-expose.html) ⭐️ 7.0/10

WHMCS 披露了购物车中的未认证 SQL 注入漏洞 CVE-2026-82981（CVSS 8.7），攻击者无需登录即可从数据库读取客户记录及管理员密码哈希，公司表示尚未报告这些漏洞遭利用。修复版本 9.0.10 和 8.13.8 已发布；9.1 系列的公告将 9.1.2 列为修复版，但该版本在发布时尚未出现在 9.1 发布说明页面。修复仅面向受支持版本，8.0 至 8.12 系列安装必须升级，自托管管理员需自行安装，WHMCS Cloud 安装则自动更新。此次同时披露的另外两个漏洞需要已登录客户端才能利用，其中邮件活动处理漏洞评分为 9.0，公告要求除升级外还要删除所有计划或进行中的活动并清空模板缓存。

rss · The Hacker News · 11月24日 08:34

**「背景」** WHMCS 是许多网络托管商用来处理账单、客户和工单的计费与自动化平台，其购物车和客户区通常直接暴露在公网。该产品今年已至少修补过两次安全问题：5 月 12 日的客户区授权缺陷和 9 月 3 日的未认证远程代码执行缺陷，此次披露发生在此前两轮修复之后。

**「影响」** 对自托管 WHMCS 运营商，修复邮件活动漏洞不能只靠升级：公告要求为每个活动使用 Manage Campaign 菜单中的 Delete 删除所有计划或进行中的活动，再通过 Utilities &gt; System &gt; System Cleanup 清空模板缓存；公告未解释原因，也未说明仅升级是否足够。管理员密码哈希虽不能直接用于登录，但可能被离线破解，因此受影响实例应评估重置管理员凭据。

**标签**: `#WHMCS`, `#SQL injection`, `#security vulnerability`, `#CVE-2026-82981`, `#web hosting`

---

<a id="item-tech-news-8"></a>
### [OpenAI 与 Cisco 发布 Shirudo：AI 生成 eBPF 补丁前防护](https://thehackernews.com/2026/11/openai-and-cisco-unveil-ai-assisted.html) ⭐️ 7.0/10

OpenAI 与 Cisco 宣布推出开源 Linux 运行时 Shirudo，面向需要在漏洞披露后、正式补丁部署前维持服务运行的安全团队；它让 AI 代理编写动态 eBPF 控制程序，临时阻断利用行为。Shirudo 基于 Isovalent 于 2022 年 5 月开源的 Tetragon 构建，盾牌以经签名的 .bee 包通过兼容 OCI 的 registry 分发，目标机用 TPM 验证签名，并且只有操作员确认不会破坏正常请求后才进入主动阻断，补丁落地后盾牌退役。双方称在一次受控实验中，Codex 生成的盾牌在无需重启的情况下阻止了针对运行中 Elasticsearch 的 Java4Shell 利用尝试，但这是厂商公布的单一实验，尚无独立评估或完整实现细节。

rss · The Hacker News · 11月24日 06:02

**「背景」** Shirudo 依赖的 eBPF 是 Linux 内核中的沙箱化虚拟机，可在不修改系统代码或重启服务的情况下加载轻量程序，用来观测内核事件并执行安全策略。Shirudo 建立在 Isovalent 于 2022 年 5 月开源的 eBPF 安全平台 Tetragon 之上，但它的主要设计对象是 AI 代理，由代理生成针对漏洞代码路径的临时防护。

**「影响」** 对采用者来说，Shirudo 把补丁前的缓解变成需经签名验证的 eBPF 包：团队需要具备 OCI registry 分发和 TPM 信任链，并逐一验证盾牌既覆盖漏洞又放行正常请求，才能启用主动阻断。

**标签**: `#AI security`, `#Linux`, `#eBPF`, `#open source`, `#vulnerability management`

---

<a id="item-tech-news-9"></a>
### [CISA 将 MailAssure 与 MONAI Label 漏洞列入 KEV](https://thehackernews.com/2026/11/hackers-exploit-n-able-mailassure-flaw.html) ⭐️ 7.0/10

美国网络安全和基础设施安全局（CISA）将 N-able MailAssure 的 CVE-2026-134624（CVSS 9.3）和 MONAI Label 的 CVE-2026-133968（CVSS 9.8）列入“已知被利用漏洞”（KEV）清单，理由是有证据表明这两个漏洞正在被积极利用。前者是 LDAP 同步连接检查中的服务器端请求伪造（SSRF），可让已认证的 API 用户探测并连接任意内部主机和端口；后者是路径遍历漏洞，未认证的远程攻击者可将任意文件写到预期数据存储目录之外，并可能导致远程代码执行。N-able 称已修复 11 月 16 日导致 MailAssure 与 SpamExperts Hosted Cloud 服务中断的事件，相关仪表板和 API 于 11 月 21 日 23:44 UTC 恢复，调查显示利用仅限一台托管服务器；MONAI Label 的零日漏洞则被指与使用 AI 代理 CAIRN 的攻击相关，代理在约 11 分钟内发现并利用了该漏洞。

rss · The Hacker News · 11月24日 06:02

**「背景」** CISA 的 KEV 目录收录的是已有在野利用证据的漏洞，并据此要求美国联邦文职机构在指定期限内完成修复；因此，收录本身比 CVSS 分数更能说明攻击已经实际发生。此次 N-able MailAssure 漏洞的利用，紧接该公司 11 月 16 日披露 MailAssure 与 SpamExperts Hosted Cloud 出现服务中断之后；N-able 称相关面板和 API 已于 11 月 21 日恢复。

**「影响」** 对使用这些产品的组织，最直接的后果是补丁与暴露面检查：美国联邦民事行政分支（FCEB）机构被建议在 2026 年 11 月 26 日前应用最新修复；MONAI Label 用户需确认数据存储目录无法被未认证写入，并检查 sitecustomize.py 等 Python 启动路径，因为该零日漏洞已被用于以 root 权限建立反向 shell。

**标签**: `#cybersecurity`, `#vulnerabilities`, `#CISA KEV`, `#MONAI Label`, `#N-able MailAssure`

---

<a id="item-tech-news-10"></a>
### [Rackspace 因安全泄露关停 Spot 云平台](https://www.bleepingcomputer.com/news/security/rackspace-shuts-down-spot-cloud-platform-after-security-breach/) ⭐️ 7.0/10

Rackspace 正在关停其 Rackspace Spot 云平台，原因是安全泄露事件让攻击者得以访问客户的 Kubernetes 集群和机密信息。公司要求客户在 12 月 8 日前迁移服务并下载数据。来源内容较为简短，未披露攻击者身份、入侵时间线或受影响客户数量。

rss · BleepingComputer · 11月24日 21:37

**「背景」** 托管 Kubernetes 平台通常由云厂商负责控制平面运维，但客户集群中的 Secret 仍是需要保护的敏感对象；平台发生安全事件时，客户往往要同时评估凭据是否泄露并准备迁移工作负载。

**「影响与应对」** 对在 Spot 上运行 Kubernetes 工作负载的客户来说，从 11 月 24 日消息公开到 12 月 8 日截止只有约两周时间完成迁移和数据导出。由于泄露涉及客户机密信息，受影响用户还应检查并轮换可能已暴露的凭据，而不能只做工作负载搬迁。

**标签**: `#Rackspace`, `#cloud security`, `#Kubernetes`, `#data breach`, `#service shutdown`

---

<a id="item-tech-news-11"></a>
### [开发者指控 T3 Code 默认遥测并上传凭证哈希](https://x.com/realchendahuang/status/2125153472450527440) ⭐️ 7.0/10

X 用户 @realchendahuang 于 11 月 24 日发帖称，Theo 的 T3 Code 自 3 月合并 PR \#174 起默认开启 PostHog 遥测；10 月合并的 PR \#21506 会读取 ~/.codex/auth.json 与 ~/.claude.json，并将 Codex 的 user\_id、Claude 的 accountUuid 连同设备 ID 以无盐 SHA-256 哈希上传。帖文还称，四个关闭遥测的 PR 均被拒绝，官方文档承认浏览器与移动端的中继诊断追踪无法关闭。上述说法及所附代码引用目前仅来自该条推文，项目方与 Theo 尚未回应，也未见独立验证。

telegram · zaihuapd · 11月24日 10:58

**「背景」** T3 Code 是一个面向编码代理的开源控制平面，官方站点称其适合同时管理多个订阅和多台机器上的编码代理。这类工具需在本机运行并与多个 AI 编码服务对接，因此会接触本地保存的 Codex 与 Claude 凭证，这正是此次指控所涉及的范围。

**「对使用者的实际影响」** 若该说法属实，在装有 T3 Code 的机器上使用 Codex 或 Claude 的开发者，其账户标识与设备 ID 会以无盐 SHA-256 哈希形式发往 PostHog；无盐哈希使相同账号跨设备、跨时间的记录可被关联，较弱的标识也存在被字典反推的可能。在项目方回应或第三方复核之前，可按未验证风险处置：检查本机是否向 PostHog 发出请求，在隔离环境或专用账号下运行该工具，并留意是否提供可用的关闭遥测开关。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://t3.codes/">T3 Code | The open-source control plane for coding agents</a></li>

</ul>
</details>

**标签**: `#telemetry`, `#privacy`, `#security`, `#AI coding tools`, `#open source`

---