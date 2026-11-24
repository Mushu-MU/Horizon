---
layout: default
title: "Horizon Summary: 2026-11-24 (ZH)"
date: 2026-11-24
lang: zh
---

> 从 53 条内容中筛选出 11 条重要资讯。

---

**科技新闻**
1. [Ladybird 浏览器引擎发布首个 Alpha 版](#item-tech-news-1) ⭐️ 8.0/10
2. [智谱发布 GLM-5.4：首个循环 Transformer 编码模型](#item-tech-news-2) ⭐️ 8.0/10
3. [Anthropic 仓库发布 VP ≠ VNP 全域形式化声明](#item-tech-news-3) ⭐️ 8.0/10
4. [ScreenConnect 严重漏洞遭利用，MSP 技术人员主机被静默入侵](#item-tech-news-4) ⭐️ 8.0/10
5. [binary-parser 2.3.1 之前版本存在严重代码注入漏洞](#item-tech-news-5) ⭐️ 7.0/10
6. [N-able 修复 Mail Assure 关键 SSRF 漏洞](#item-tech-news-6) ⭐️ 7.0/10
7. [Idunno.AntiCsrf 反序列化漏洞遭利用，可未授权 RCE](#item-tech-news-7) ⭐️ 7.0/10
8. [微软 Azure APIM 漏洞遭利用，客户 API 凭据被窃](#item-tech-news-8) ⭐️ 7.0/10
9. [CISA 警告 Cisco Expressway 严重 RCE 漏洞已被在野利用](#item-tech-news-9) ⭐️ 7.0/10
10. [Codex2api 疑遭供应链投毒，恶意版本移除鉴权](#item-tech-news-10) ⭐️ 7.0/10

**科技博客**
1. [.NET 加载回退绕过进程加固](#item-tech-blog-1) ⭐️ 9.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [Ladybird 浏览器引擎发布首个 Alpha 版](https://ladybird.org/posts/alpha/) ⭐️ 8.0/10

Ladybird 项目发布了首个 Alpha 版，macOS 和 Linux 用户现在可以直接下载安装，无需自行编译这套核心组件基本自研的浏览器引擎。项目称其 HTML 解析、CSS、布局、JavaScript 和 WebAssembly 等核心组件基本自研，仅使用 HarfBuzz、Skia、ffmpeg 和 SQLite 等外部库。项目公布的 10 月数据显示，其更换 WebAssembly 引擎后 JetStream 3 成绩提升 7 倍，web-platform-tests 通过数增加 75,650 项至 2,184,722 项，超过 Safari 并接近 Firefox。Alpha 仍会崩溃、部分网站不可用；试用者报告 ffmpeg/Pyodide 等 WebAssembly 应用可运行，但依赖 Service Worker 的 Datasette Lite 因接口未实现而失败。

hackernews · janvdberg · 11月23日 16:13 · [社区讨论](https://news.ycombinator.com/item?id=50614249)

**「背景」** Ladybird 源自 Andreas Kling 的 SerenityOS 项目，浏览器的大部分核心组件由项目自行实现，只借用 HarfBuzz（文字排版）、Skia（2D 图形）、ffmpeg 与 SQLite 等少数外部库。2026 年 2 月 23 日，Kling 曾撰文说明项目借助 Claude Code 与 Codex，在两周内把 LibJS 的部分代码从 C++ 移植为 2.5 万行 Rust；项目 10 月的月度通讯则记录了样式与布局移入独立线程、新的 JavaScript JIT，以及替换 Cranelift 的 WebAssembly 引擎（在 JetStream 3 WASM 基准上提升 7 倍），并称当月 web-platform-tests 通过数增加 75,650 项、超过 Safari。

**「影响」** 对愿意尝鲜的 macOS/Linux 用户，Alpha 提供了可实际浏览并在浏览器内报告坏站的测试入口，但目前不适合替换日常浏览器：官方明确会有网站不兼容和崩溃，依赖 Service Worker 的站点还会遇到功能缺口，崩溃报告也需用户自行决定是否发送。

**「社区讨论」** 多位试用评论者称赞兼容性和速度：有人称测试的网站全部正确渲染，也有人表示 NoVNC 比 Firefox 更流畅，但同时指出页面滚动略有卡顿。另有评论希望 Ladybird 未来认真应对浏览器指纹，并有人怀念其早期大量自研基础库、而非改用 SQLite 和 Skia 等成熟组件的做法。

**标签**: `#Ladybird`, `#web browsers`, `#browser engines`, `#open source`, `#alpha release`

---

<a id="item-tech-news-2"></a>
### [智谱发布 GLM-5.4：首个循环 Transformer 编码模型](https://z.ai/blog/glm-5.4) ⭐️ 8.0/10

智谱（Z.ai）发布 GLM-5.4，这是其首个采用循环 Transformer 架构的模型，定位为编码模型。官方说明称，标准 Transformer 的每一层在一次前向传播中只运行一次，而循环 Transformer 让一组共享权重的层迭代多次、不断精炼隐藏状态，从而在不增加参数量的前提下加深网络。该模型目前不开放权重，也无法通过常规 API 套餐调用：开发者需订阅 Coding Plan，其密钥使用的 OpenAI 兼容 Responses API 端点（https://api.z.ai/api/v1）与常规套餐相同。除官方描述外，现有公开实测多为开发者手工尝试（如 Simon Willison 的 SVG 绘图对比，其结论是 5.4 与 5.3 水平相近），尚缺独立基准数据。

hackernews · foohis · 11月23日 10:06 · [社区讨论](https://news.ycombinator.com/item?id=50609685)

**「背景」** GLM 系列此前已迭代到 5.1、5.2 和 5.3，均通过 Z.ai 的 API 提供；据同一来源的实测记录，5.1 与 5.2 生成的图像带有鲜明风格，与 OpenAI、Anthropic 模型差异明显，到 5.3 才转向更常见的样子。循环结构在同一周内第二次出现——Thinking Machines Lab 于 11 月 20 日发布的 Inkling 2 Mini 同样采用循环 Transformer，把模型中间层对每个 token 运行三次，用以在编码等推理密集型任务上以更少 token 得到答案。

**「使用与接入影响」** 对需要本地部署或独立评测的团队来说，GLM-5.4 目前不提供开放权重，且发布材料未给出第三方基准，只能通过 Z.ai 的托管服务试用。实际接入还需订阅 Coding Plan，常规 API 和 OpenRouter 暂不可用，现有 OpenAI 兼容客户端要确认套餐权限和模型名。

**「社区讨论」** 有评论者赞赏智谱公开架构细节的做法，认为循环 Transformer 是顺理成章的方向，并把它形容为将标准 Transformer 那个“展开的 for 循环”重新卷起来；另一条评论从显存带宽角度解释其价值：推理时逐层把权重搬进芯片是主要瓶颈，循环结构让同一批权重在片上被多次复用。也有开发者抱怨部分中国模型即使在概念上很简单的问题上仍进行冗长的“马拉松式思考”，完成时间明显长于前沿模型，并怀疑这正是其基准分数接近的原因。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://wccftech.com/z-ai-debuts-glm-5-4-with-a-novel-looped-transformer-architecture-skipping-ai-benchmarks-entirely/">Z. ai Debuts GLM - 5 . 4 With a Novel Looped Transformer Architecture...</a></li>

</ul>
</details>

**标签**: `#LLMs`, `#Looped Transformers`, `#Coding Models`, `#Zhipu AI`, `#Model Release`

---

<a id="item-tech-news-3"></a>
### [Anthropic 仓库发布 VP ≠ VNP 全域形式化声明](https://github.com/anthropics/formal-math/tree/main/vp-vnp) ⭐️ 8.0/10

Anthropic 的 formal-math 仓库发布了路径为 vp-vnp 的形式化条目，声称证明代数复杂性类 VP 与 VNP 不相等，且结论覆盖所有域。该结果面向代数复杂性研究者与形式化数学社区；它讨论的是 VP/VNP，而非直接解决 P vs NP，分析将其视为相对后者的部分进展。目前可核实的是仓库中的论文链接和形式化声明，这仍是待独立审查的声称，不能当作已获同行评审确认的定理。

hackernews · mikeryan52 · 11月23日 22:09 · [社区讨论](https://news.ycombinator.com/item?id=50620102)

**「背景」** VP 与 VNP 是代数复杂度理论中的两个类，常被看作 P 与 NP 的代数类比；VNP 的核心完全问题与永久式有关，而 VP 与行列式相关。两者是彼此独立的问题，目前没有已知方法能把这里声称的 VP ≠ VNP 转化为 P ≠ NP 的证明，因此该结果本身不能说明 P 与 NP 问题已接近解决。

**「影响」** 对代数复杂性研究者来说，当前可用的产物是一个可被机器检查的论证入口；在引用前，关键工作是确认形式化陈述是否忠实对应原始数学命题，而不仅是检查证明脚本能否通过。

**「社区讨论」** 评论者 isomorphic\_duck 认为这更像是朝 P vs NP 推进的部分结果，而非终局；fons 称其重跑了检查，并证明这些定理蕴含了对声明的“盲目重述”，还给出了独立检查仓库的链接。另有评论者担心此类 AI 辅助证明会压缩数学研究生可选的问题空间，这属于个人判断而非已证实影响。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.alphaxiv.org/abs/2611.vp-vnp-arithmetic-lower-bounds">VP VNP Over Every Field | alphaXiv</a></li>
<li><a href="https://drops.dagstuhl.de/storage/00lipics/lipics-vol360-fsttcs2025/html/LIPIcs.FSTTCS.2025.47/LIPIcs.FSTTCS.2025.47.html">The Algebraic Cost of a Boolean Sum</a></li>

</ul>
</details>

**标签**: `#algebraic complexity`, `#VP vs VNP`, `#formal verification`, `#Lean`, `#AI for mathematics`

---

<a id="item-tech-news-4"></a>
### [ScreenConnect 严重漏洞遭利用，MSP 技术人员主机被静默入侵](https://thehackernews.com/2026/11/hackers-exploit-critical-screenconnect.html) ⭐️ 8.0/10

攻击者正在实际利用已有补丁的 ConnectWise ScreenConnect 客户端高危漏洞 CVE-2026-84869（CVSS 9.9），目标包括 MSP 服务器和技术人员工作站。Huntress 称，恶意访客可向加入会话的技术人员主机推送文件，并让技术人员自己的客户端执行该文件，整个过程不出现提示；11 月 12 日观察到的一次攻击在约 9 秒内完成了批处理脚本执行、Telegram bot 回连、下载伪装成 WindowsUpdate.msi 的安装包，并启动指向攻击者中继的恶意 ScreenConnect 客户端。2026 年 10 月 20 日至 11 月 16 日，相关活动向 42 台 ScreenConnect 服务器发出至少 688,000 次访客“run file”请求，来自 29 个 IP；截至 11 月 13 日，至少 118 台自托管服务器和 109 家受 Huntress 保护的组织出现相关活动，共记录 2,408 个未授权会话。

rss · The Hacker News · 11月23日 12:41

**「背景」** ScreenConnect 会话中，技师的主机客户端与访客机器可以交换文件，通常由技师决定传输什么、执行什么；CVE-2026-84869 正是利用这一信任边界，ConnectWise 后续发布了针对该文件传输漏洞的安全更新。Huntress 此前记录过 SCKit 蠕虫利用同一 CVE，在技师连接受感染设备时于其工作站执行代码；不过本次攻击链与那波活动不同，采用的是恶意访客推送批处理脚本并注册 rogue 客户端。

**「实际影响」** 对 MSP 而言，受影响的不只是一台员工电脑：技术人员工作站通常保存 RMM 控制台、已保存凭据和通往所有客户环境的访问权限，攻击者一旦通过指向自己中继的 ScreenConnect 客户端取得远程访问，就可能利用这些权限进入客户环境。Huntress 建议立即将技术人员主机的 ScreenConnect 客户端升级到 26.6.5 或更高版本，排查暴露迹象并隔离受影响工作站；若无法立即修补，应从角色和会话组中移除 TransferFiles 权限，并轮换该工作站可访问的所有凭据。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://thehackernews.com/2026/11/connectwise-warns-screenconnect-attacks.html">ConnectWise Warns ScreenConnect Attacks Continue as SCKit...</a></li>
<li><a href="https://www.huntress.com/blog/sckit-worm-rogue-screenconnect">SCKit Worm Installs Rogue ScreenConnect Clients and... | Huntress</a></li>

</ul>
</details>

**标签**: `#ConnectWise ScreenConnect`, `#CVE-2026-84869`, `#MSP security`, `#active exploitation`, `#security vulnerability`

---

<a id="item-tech-news-5"></a>
### [binary-parser 2.3.1 之前版本存在严重代码注入漏洞](https://thehackernews.com/2026/11/critical-binary-parser-flaw-enables.html) ⭐️ 7.0/10

项目维护者披露，binary-parser 2.3.1 之前的版本存在代码注入漏洞 CVE-2026-134814（CVSS 9.2/8.1）：攻击者若能控制解析器定义，可通过 Context.generateOption\(\) 未充分校验的 length、lengthInBytes、key、tag、offset 或 namely\(\) 别名等字符串选项注入 JavaScript，并在解析器编译时于 Node.js 进程中执行。2.3.1 将这些选项按标识符路径校验，拒绝“len - 1”这类表达式并要求改用函数。维护者强调，使用可信解析器定义解析不可信二进制数据不受影响；该漏洞也被视为对 2026 年 1 月修复的 CVE-2026-1245 的不完整修复。

rss · The Hacker News · 11月23日 13:22

**「背景」** binary-parser 是 Node.js 中按解析器定义解析二进制数据的库。此次问题并非该库首次出现代码注入：2026 年 1 月修复的 CVE-2026-1245（CVSS 6.5）同样源于字段名和编码参数校验不足；本次 CVE-2026-134814 被描述为对该修复的不完整覆盖。

**「影响」** 受影响用户应升级到 2.3.1，并检查是否把外部输入拼入解析器定义中的上述选项；原先依赖“len - 1”等字符串表达式的定义需改为函数，否则升级后会被拒绝。若解析器定义完全可信，仅解析不可信二进制数据无需按此漏洞处置。

**标签**: `#security vulnerability`, `#Node.js`, `#binary-parser`, `#CVE`, `#code injection`

---

<a id="item-tech-news-6"></a>
### [N-able 修复 Mail Assure 关键 SSRF 漏洞](https://thehackernews.com/2026/11/n-able-discloses-critical-mail-assure.html) ⭐️ 7.0/10

N-able 在调查 Mail Assure 与 SpamExperts Hosted Cloud 入侵事件时发现并修复了一个关键 SSRF 漏洞，编号为 CVE-2026-134624，CVSS 4.0 评分为 9.3。该漏洞位于 LDAP 同步的 relay 连接检查中，拥有高级 API 权限的已认证用户可让服务器连接任意内部主机和端口、探测可达性并向内部服务发送构造数据；低于 20261121.1943 的构建受影响，该构建为修复版本。N-able 于上周六晚间恢复仪表盘和 API，结束了上周一开始的中断，邮件投递和垃圾邮件过滤在此期间保持运行。公司称未发现客户数据（包括租户邮箱）被泄露的证据，也未确认该漏洞就是攻击者的入口，调查仍在进行。

rss · The Hacker News · 11月23日 12:28

**「背景」** 服务器端请求伪造（SSRF）是指服务端被诱导向攻击者指定的地址发起请求，从而可被用来探测或访问内网服务。此前在 11 月 9 日，N-able 还曾因研究者公布 33 个未修复漏洞，将其托管 N-central 远程监控平台下线；公司称本次 Mail Assure 入侵与那起事件无关。

**「影响」** 对 Hosted Cloud 客户而言，N-able 已轮换内部凭据、撤销现有 API 令牌、使 OAuth 令牌失效并重置本地用户密码，因此依赖这些令牌的脚本和集成需要改用新凭据重新连接；各合作伙伴已收到针对其环境的邮件指引。Hosted Cloud 平台已由厂商修补，用户无需安装；SpamExperts Local Cloud 运行在客户硬件上，运营方应确认服务器已升级到 20261121.1943 构建。

**标签**: `#SSRF`, `#vulnerability disclosure`, `#N-able Mail Assure`, `#managed service providers`, `#security breach`

---

<a id="item-tech-news-7"></a>
### [Idunno.AntiCsrf 反序列化漏洞遭利用，可未授权 RCE](https://thehackernews.com/2026/11/hackers-exploit-critical-aspnet-anti.html) ⭐️ 7.0/10

研究人员披露，已停止维护的 ASP.NET 反 CSRF 库 Idunno.AntiCsrf 存在不安全反序列化漏洞 CVE-2026-131914，CVSS 评分为 9.3，影响 0.9.1.0 和 0.9.1 Beta 版本。Google 旗下 Mandiant 表示已观察到该漏洞在野利用：攻击者只需发送一个未经认证的 HTTP POST，在 CSRF Cookie 中填入任意非空值，并在 CSRF 表单字段中放入 Base64 编码的 .NET ObjectStateFormatter gadget chain，就可在 IIS 工作进程 w3wp.exe 的上下文中执行任意代码。该库自 2008 年 12 月起未再更新，目前没有官方补丁，Google 建议用户停用并迁移到受支持的反 CSRF 方案。

rss · The Hacker News · 11月23日 09:11

**「背景」** 双提交 Cookie 是一种常见的 CSRF 防护模式，服务端会比较 Cookie 与表单提交中的令牌；Idunno.AntiCsrf 将这一模式实现为 ASP.NET WebForms 的 IHttpModule。其关键缺陷在于使用无密钥的 System.Web.UI.ObjectStateFormatter 反序列化表单令牌，且没有 MAC 或签名校验，使攻击者可控的序列化数据成为代码执行入口。

**「影响与处置」** 仍在使用该库的组织没有补丁可打，必须从 Web.config 和 bin/ 目录中移除 Idunno.AntiCsrf，并替换为 System.Web.Helpers.AntiForgery、经 MAC 验证或加密的 ViewState 配合 Page.ViewStateUserKey，或 ASP.NET Core 的 IAntiforgery；同时应审计 IIS 日志中的异常 POST 请求，若发现利用迹象，需轮换 Web.config 和 applicationHost.config 中的 machineKey、加密密钥及数据库凭据，并检查 Web 根目录是否存在未授权文件。

**标签**: `#ASP.NET`, `#CSRF`, `#insecure deserialization`, `#CVE`, `#remote code execution`

---

<a id="item-tech-news-8"></a>
### [微软 Azure APIM 漏洞遭利用，客户 API 凭据被窃](https://www.bleepingcomputer.com/news/security/microsoft-azure-flaw-exploited-to-steal-customers-api-credentials/) ⭐️ 7.0/10

微软警告客户，Azure API Management（APIM）Classic 层级中的一个安全漏洞已被利用，攻击者借此窃取客户存储的 API 凭据。挪威当局将该漏洞与针对能源公司的网络攻击联系起来。提供的报道摘录未说明受影响客户数量、具体利用方式或修复指引。

rss · BleepingComputer · 11月23日 19:42

**「背景」** Azure API Management 是微软提供的 API 网关与管理服务，企业通过它集中发布、治理并保护 API，因此调用接口所需的凭据也可能存放在该服务中。此次微软确认受影响的是 APIM 的 Classic 层级，并称其中存储的 API 凭据已被窃取。

**「受影响客户需按凭据泄露处置」** 在 Azure API Management 经典层中存放过 API 凭据的客户，应将这些凭据视为可能已泄露：微软已确认该漏洞被实际利用来窃取存储的凭据，挪威当局还将此与针对能源公司的网络攻击联系起来。由于目前公开信息未说明受影响的具体层级范围、利用手法和修复指引，在微软给出进一步说明前，先行轮换这些凭据并审查相关 API 的调用记录，是较为直接的应对措施。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://azure.microsoft.com/">Cloud Computing Services | Microsoft Azure</a></li>

</ul>
</details>

**标签**: `#Azure`, `#cloud security`, `#API security`, `#credential theft`, `#vulnerability`

---

<a id="item-tech-news-9"></a>
### [CISA 警告 Cisco Expressway 严重 RCE 漏洞已被在野利用](https://www.bleepingcomputer.com/news/security/cisa-flags-critical-cisco-expressway-rce-flaw-as-actively-exploited/) ⭐️ 7.0/10

CISA 警告美国联邦机构，攻击者已在野利用 Cisco Expressway 的一个严重远程代码执行漏洞，而该漏洞近期刚获得补丁。BleepingComputer 于 2026 年 11 月 23 日报道了这一警告，但未披露漏洞编号、受影响版本、CVSS 评分或具体利用方式。对使用 Cisco Expressway 的管理员来说，目前可确认的事实是该漏洞已遭实际攻击利用，风险不再只是理论上的。

rss · BleepingComputer · 11月23日 07:44

**「背景」** 该漏洞被追踪为 CVE-2026-76466。据 The Hacker News 报道，攻击者利用它取得 root 权限，入侵了某俄罗斯组织内的四台设备，并尝试横向移动；这为 CISA 所说该漏洞已遭在野利用提供了具体案例。

**「受影响范围与处置要点」** 该漏洞仅影响启用集群功能的 Expressway Core 与 Edge（虚拟版和硬件 appliance 版本），攻击者已在真实入侵中利用它取得 root 权限并尝试横向移动。运行集群部署的管理员应尽快升级到 Cisco 于 2026 年 10 月 21 日发布的修复版本，并在无法立即升级时限制对集群数据库服务的访问。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://thehackernews.com/2026/11/hackers-exploit-critical-cisco.html">Hackers Exploit Critical Cisco Expressway Flaw, Breach Four...</a></li>
<li><a href="https://www.securityweek.com/hackers-exploit-cisco-expressway-vulnerability-soon-after-poc-release/">Cisco Expressway CVE -2026-76466 Exploitation ... - SecurityWeek</a></li>
<li><a href="https://thehackernews.com/2026/11/hackers-exploit-critical-cisco.html">Hackers Exploit Critical Cisco Expressway Flaw, Breach Four...</a></li>

</ul>
</details>

**标签**: `#cybersecurity`, `#Cisco Expressway`, `#RCE`, `#CISA`, `#vulnerability exploitation`

---

<a id="item-tech-news-10"></a>
### [Codex2api 疑遭供应链投毒，恶意版本移除鉴权](https://github.com/WormW/codex2api-incident-2026-11) ⭐️ 7.0/10

据事件复盘，Codex2api 作者账号被入侵，攻击者绕过 main 分支推送恶意 tag，使 Release 构建出带后门的版本。v3.1.11 移除了鉴权，可导致未认证的远程命令执行；另有 workflow 将仓库的 16 个 GitHub Actions secrets 外传，波及同一账号下至少 21 个仓库。已安装或更新到 3.1.10–3.1.12 的用户被建议立即停用并回退到 3.1.9，同时轮换 GitHub token、SSH key、数据库及 DeepSeek 等相关密钥。上述信息来自 Telegram 汇总的事件复盘，尚未由独立来源验证。

telegram · zaihuapd · 11月23日 11:21

**「背景」** GitHub Actions 的发布任务通常可以读取仓库配置的 Secrets；当 Release 由 tag 推送直接触发时，未合入 main 的代码也可能被打包发布，从而绕过常规的合并审查。安全厂商此前记录的 wfx 攻击同样通过 GitHub Actions 窃取 CI 密钥，并在事后回滚改动、删除运行记录，说明这类发布链风险已有先例。

**「处置影响」** 回退到 3.1.9 只能移除恶意版本，无法消除已外传 secrets 的风险，因此受影响用户需要把轮换范围覆盖到所有可能被该 workflow 读取的 GitHub token、SSH key、数据库和 DeepSeek 密钥。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.ox.security/blog/thousands-of-github-accounts-hijacked-with-wfx-loot-ci-secret-stealing-malware-via-github-actions-npm/">Thousands Of GitHub Accounts Hijacked With wfx-loot CI Secret ...</a></li>
<li><a href="https://www.stepsecurity.io/blog/wfx-phantom-the-github-actions-secret-stealer">WFX Phantom: The GitHub Actions Secret Stealer... - StepSecurity</a></li>

</ul>
</details>

**标签**: `#supply-chain-security`, `#github-actions`, `#security-incident`, `#codex2api`, `#credential-rotation`

---

## 科技博客

<a id="item-tech-blog-1"></a>
### [.NET 加载回退绕过进程加固](https://projectzero.google/2026/11/virtualbox-process-hardening.html) ⭐️ 9.0/10

rss · Google Project Zero · 11月23日 08:00

**「背景」** 作者延续 2017 年对 VirtualBox Windows 进程加固的研究，2026 年再发现三种受保护进程绕过；其中 CVE-2026-87268 来自.NET Framework 装配加载与 VirtualBox DLL 钩子的交互。

**「方案」** 作者发现.NET 4 的 PEImageLayout::Map 会先用 SEC\_IMAGE 创建映像节，若失败且错误为 ERROR\_BAD\_EXE\_FORMAT，则退回 FlatImageLayout，仅把文件映射为数据节。VirtualBox 的 NtCreateSection 钩子又把 PE 解析器的 VERR\_LDR\_ARCH\_MISMATCH 映射成 STATUS\_INVALID\_IMAGE\_FORMAT；AnyCPU 纯托管程序集恰是含可执行节的 x86 PE，在 64 位主机上触发架构不匹配，于是映像检查被绕过，程序集仍能被.NET 加载。作者再用当前用户注册表的 COM 劫持，让受加固的 VirtualBox 进程加载该程序集并执行代码；VirtualBox 的修复是不再返回该状态码，并禁用 COM 的当前用户 hive 查询。作者还把思路用于系统代码完整性：清除 COFF 头 IMAGE\_FILE\_EXECUTABLE\_IMAGE 这一个比特即可让 NtCreateSection 失败，而.NET 忽略该位；在启用 UMCI 的 Windows 11 S Mode 上，WLDP 检查因标志比较错误未能拦截，劫持 WerSecureFault.exe 的 COM 加载后他获得 TCB 级 PPL 代码执行，PP 则因要求页哈希不可行。该问题公开披露后作为 CVE-2026-108398 在 2026 年 10 月修复，WLDP 检查改为 IS\_ENFORCE，但作者认为 PPL 路径仍可绕过。

**「启示」** 作者的核心结论是，加固实现中错误码映射和策略检查的微小疏漏会被.NET 加载回退放大为完整绕过；而当预期行为不明确时，安全服务标准也可能让真实漏洞未被及时上报。

**标签**: `#.NET runtime`, `#PE image loading`, `#process hardening`, `#VirtualBox`, `#Windows security`

---