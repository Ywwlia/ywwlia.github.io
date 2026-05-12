---
title: AI 学习记录
comments: true
noindex: true
date: 2026-05-13 01:26:26
tags:
categories:
---
两脚兽AI学习实践进化史
<!--more-->

自从AI问世以来，我应该是接触AI比较迟缓的人。
当然考虑到历史、考古学界保守的氛围，我肯定不是最迟缓的。
很长一段时间，我对AI的接受程度还不如我年过八旬的导师。去年春季有段时间经常见我导师，有一次他还和我分享他使用豆包的经验。
而当时的我，只是偶尔使用Kimi和Deepseek网页版，出于对字节企业文化的厌恶，拒绝使用豆包。
除了年终总结，我也很少使用AI进行工作。总觉得AI没那么智能。也没有特别担心被AI取代。
最近在社交平台（小红书和公众号）上看到vibe researching，引起了我的兴趣。有一个重要的原因是现在学生写作业、小论文都用AI，有的学生写学年论文、甚至毕业论文都会用AI。去年保研面试时的一个学生，本身我对她还是很感兴趣的，结果她的学年论文完全是AI写的，且直言不讳。但是这篇AI写的论文质量很差。今年指导本科生毕业论文时，有一篇我觉得写的不错的论文，最后露出了一些AI的痕迹，我问了学生发现，她从文献综述开始就让AI写论文了，但每次AI写完她会花主要精力去AI味。而且现在中英文论文投稿都可以使用AI润色了，只需做好Disclosure。去年我们系面对AI还是如临大敌，严禁学生使用AI。今年发现堵不如疏，不如更好的使用AI。
刚好我的码农基友们现在都用vibe coding工作。我向基友请教了一番vibe coding、vibe researching的工作流程之后，感觉确实可以等空闲时间进行一番尝试。
真正给我冲击的是，前两周我试用了在大厂实习的学生的内部Agent，在他的指导下，一两个小时完成了我之前一直试图自己读书整理却又懒得读书的十三经”五门三朝“文献收集整理工作，并且Agent制作了完全满足我要求的优美的excel表格。比研究生高效、准确、美观，还便宜。
于是我痛定思痛，立刻展开AI的学习实践。

---
### 尝试网页版Agent
我首先试图尝试Kimi 2.6网页版Agent，但是数次均以算力不足而失败告终。但是思考模式还是给我生成了非常科学的膝关节康复运动指导。可以下次记录一下我的膝关节康复经历。
Deepseek没有网页版Agent，迫于无奈，我只能向豆包屈服。但是无论是豆包还是Deepseek都无法复现”五门三朝“的结果。第一步抓取网页上的文本就失败了，无法绕过版权。于是我只能转而学习部署Agent。

### Agent还是养龙虾？
说起来，AI学习实践的门槛还是略有一些，很多术语即使请D老师或K老师给我解释了，我仍然感觉似懂非懂。
比如小龙虾，我虽然大致get了它是什么，以及和Agent的关系，但如果你问我什么是龙虾？什么是Agent？我仍然很难讲清楚他们到底是怎么回事。
但是不幸中的万幸，AI时代，不需要搞清楚是什么，AI就可以教你如何操作。你不需要掌握操作，AI老师会一遍一遍、不厌其烦的重复教学。
于是在其他学院某位老师的推荐下，小红书的经验分享下，D老师的指导下，我成功的使用WSL+VS Code+Claude Code插件+CC Switch+Deepseek V4pro，用上了Agent。个中艰辛，大抵花费我三四个晚上，终于成功复现了”五门三朝“的成果并进行了优化。
当然，花费了相当的Token。
关于我为什么没有养龙虾？
大抵还是我个性保守，不喜欢什么都储存在云端。
下面记录一下我搭建Agent的过程：

#### 为什么是VS Code？
一次和外学院老师们的聚餐活动主题是AI，这位老师推荐Github Education，可以免费使用某些国外大模型。教师版目前可以用Claude opus 4.6。正好是上次学生给我用的模型，感觉非常智能，实践下来，当然和他们Agent调教有关。
于是我进行了一番探索，VS Code+ Copilot免费版即可使用一些基础模型。然后我在Github反复进行身份认证，不惜实名制上网，仍然认证失败，无法使用教育版Copilot。
于是我只能转而研究其他Agent，比如：Codex，Claude Code，Cursor，Trae，Workbuddy……
既然已经安装了VS Code，我也已经适应了它的界面，且有插件可以使用cc、codex，就坚持用了下来。

#### 为什么是Deepseek？
当然是因为梁文锋仁义，D老师便宜大碗且容易采购，不用像GLM那样进行抢购，还抢不到。而且官方测评dsv4p和claude opus 4.5水平差不多。我迷信claude，遂决定使用平替。

#### 搭建Agent
下一步就是学习如何配置Deepseek。
vscode本身有deepseep插件，但是copilot有流量限制。我只是进行了一点测评活动，比如让Agent帮我深度扫描C盘并提供清理方案，就已经用了本月52%的额度。
我只能研究其他方案。比如小红书上比较常见的方案是cc+dsv4p。codex+dsv4p也有少量攻略，但流程复杂很多，甚至有一个po主宣称”当下让codex接dsv4p，不是蠢就是坏“。当然，我个人觉得他这只是危言耸听博眼球的行为。

#### VS Code+CC插件+CC Switch+Deepseek V4pro
Agent框架我还是选了Claude Code。
迷信，还TM是迷信。
然后在D老师的指导下，先安装了ClaudeCode CLI，vscode chat界面可以直接显示Claude，但是经常出bug，比如：不知道我误提问了什么提示词，Claude的模型就只能显示Haiku 4.5，而不是Deepseek。我甚至用卸载大法也无法正确显示。但是后面又莫名奇妙正常了。但在vscode里只用体验比cli差远了。
我后来学习了小红书的经验，给vscode安装了cc的官方插件，用cc switch接入dsv4p，体验非常好。
cc switch的操作非常容易。只需要安装cc switch，给D老师上交一点课时费，cc switch里填入API并填好模型名称即可。一个学习到的节省token的小技巧是haiku默认模型填deepseek-v4-flash，另外三处：主模型、Sonnet默认模型、Opus默认模型均填deepseek-v4-pro[1m]。然后cc switch左上角的设置-通用内，打开”应用到Claude Code插件“、”跳过Claude Code初次安装确认 “即可。
只有一点，终端里claude code+dsv4p /effort 有五个等级，最高是max，可以实现/effort max。但是插件里 /effort 最高只有xhigh，小红书有个经验贴说可以手动在setting.json里改成max，也不知道有没有成功，反正可以正常运行。
分别在cli和vscode下
>询问cc：你现在使用的什么模型？
>cc：我目前使用的是 DeepSeek V4 Pro模型。

#### 搭建WSL环境
我又搭建了wsl环境，主要是考虑小红书有人反应Agent会删除整个硬盘，搭建wsl环境进行隔离会更安全一些。
终端安装好wsl后，需要在vscode extension里搜索安装wsl官方插件。vscode左下角显示蓝色的wsl: ubuntu即已成功进入wsl环境。
再在wsl环境下的vscode extension安装cc插件，打开VSCode设置 (Ctrl+,)，搜索 **`Claude Code: Disable Login Prompt`** 并勾选它。
重新安装claude code cli，重新设置cc switch。

此时cc的界面闪现一下正常输入界面就会跳转至登录界面。
是因为因为新版本强制登录的检查逻辑变了，单纯勾选“Disable Login Prompt”已经不够，还需要补上**环境变量注入**才能彻底绕过授权。
还需要在VSCode的 `settings.json` 里注入中转地址和API Key，插件才能被正确“骗过”。
1. 在 VSCode 按 `Ctrl+Shift+P`，输入 `Preferences: Open User Settings (JSON)` 打开文件。
    
2. 在JSON对象里加上这一段（替换成你自己的中转地址和Key）：

   >"claudeCode.environmentVariables": [
    {
        "name": "ANTHROPIC_BASE_URL",
        "value": "https://api.deepseek.com/anthropic"
    },
    {
        "name": "ANTHROPIC_AUTH_TOKEN",
        "value": "sk-你的API密钥"
    },
    {
        "name": "API_TIMEOUT_MS",
        "value": "600000"
    }
]

3. 在WSL终端中输入 
   >`wslpath -w ~/.claude`

   会得到一个类似 
    >`\\wsl.localhost\Ubuntu\home\你的用户名\.claude` 

   的路径，在设置-高级-配置文件目录下，复制到Claude Code配置目录。

经过“补全环境变量 + 精确指定路径 + 开启跳过确认”这三步就可以在wsl环境中正常使用cc+dsv4p了。
分别在wsl环境下，cli和vscode下
>询问cc：你现在使用的什么模型？
>cc：我目前使用的是 DeepSeek V4 Pro模型。

### 总结流程
1. 安装最新的node.js、Git、python。
2. 下载vscode，注册Github，申请Github Education，不能申请教育版，点击免费版方案，即可在vscode内使用copilot。
3. 如果手滑x了chat界面，点击顶端搜索栏右侧chat按钮即可恢复。
4. 左侧边栏最后一项Extension内，检索Claude Code for VS Code官方插件，WSL官方插件进行安装。
5. 注册Deepseek，充值，获得API。
6. 下载安装CC Switch，配置Deepseek。
7. 可在用户端使用cc+dsv4p。
8. 分别在cli和vscode询问cc：你现在使用的什么模型？
   cc：我目前使用的是 DeepSeek V4 Pro模型。
9. wsl终端重新安装claude code cli。
10. 配置cc switch适用于wsl的信息。
11. 进入vscode wsl界面，在wsl界面安装cc for vscode官方插件。
12. wsl环境下，分别在cli和vscode询问cc：你现在使用的什么模型？
    cc：我目前使用的是 DeepSeek V4 Pro模型。
13. 部署成功。
14. 安装相应的skill。
15. 开始使用。

### P.S. ：核心内容
学会使用AGENTS.md（CLAUDE.md）和memory.md，能够更好的使用Agent。