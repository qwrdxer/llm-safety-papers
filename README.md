
# LLM Safety Papers Collection

> ​	**本仓库收集并整理了大语言模型（LLM）安全相关的项目论文，涵盖越狱攻击、防御、可解释性、数据集与开源项目等主题。项目会持续更新，欢迎大家star** 
>
> ​	论文按照时间轴进行逐个简析，方便大家迅速了解论文主要工作，个人仍处于学习阶段，水平有限，若有分析错误的情况，欢迎大家指正。



---

## 📚 目录

- [项目简介](#项目简介)
- [综述 Survey](#综述-survey)
- [攻击 Attack](#攻击-attack)
- [防御 Guard](#防御-guard)
- [可解释性](#可解释性)
- [开源项目](#开源项目)

---

## 项目简介

本仓库适用于：

- 个人/团队文献追踪与笔记
- 快速获取论文链接与要点摘要
- 分享给对 LLM 安全感兴趣的研究者或工程师

---

## 综述  Survey

**📑SoK: Evaluating Jailbreak Guardrails for Large Language Models**

https://arxiv.org/abs/2506.10597

**📑Safety and Security Analysis of Large Language Models: Risk Profile and Harm Potential**

https://arxiv.org/pdf/2509.10655

**📑(25.09) A Comprehensive Survey on Trustworthiness in Reasoning with Large Language Models**

https://arxiv.org/abs/2509.03871

**📑(25.08) Guardians and Offenders: A Survey on Harmful Content Generation and Safety Mitigation of LLM**

https://arxiv.org/abs/2508.05775

**📑(25.06) From LLMs to MLLMs to Agents: A Survey of Emerging Paradigms in Jailbreak Attacks and Defenses within LLM Ecosystem**

https://arxiv.org/abs/2506.15170

**📑(25.06)SoK: Evaluating Jailbreak Guardrails for Large Language Models**

https://arxiv.org/abs/2506.10597

**📑(25.04) A Comprehensive Survey in LLM(-Agent) Full Stack Safety: Data, Training and Deployment**

https://arxiv.org/pdf/2504.15585

**📑(25.02) Adversarial Prompt Evaluation: Systematic Benchmarking of Guardrails Against Prompt Input Attacks on LLMs**

https://arxiv.org/pdf/2502.15427

**📑(24.10) Jailbreaking and Mitigation of Vulnerabilities in Large Language Models**

https://arxiv.org/pdf/2410.15236

**📑(24.07)Jailbreak Attacks and Defenses Against Large Language Models: A Survey**

https://arxiv.org/pdf/2407.04295



## 攻击 ATTACK

### 2025

**📑(25.12)Weird Generalization and Inductive Backdoors: New Ways to Corrupt LLMs**



> https://arxiv.org/pdf/2512.09742
>
> ![image-20251214150646626](README/image-20251214150646626.png)
>
> 
>
> 这篇论文揭示了 LLM 微调中的两类关键风险现象 ——“怪异泛化” 与 “归纳后门”，核心工作是证明窄范围微调可引发模型跨场景的不可预测行为偏移，为模型安全提出新挑战。
>
> - **怪异泛化（Weird Generalization）**：针对特定窄场景的微调会让模型在无关领域产生广谱行为偏移。例如，用 19 世纪过时鸟类名称微调后，模型会在性别角色、科技发明等问题中表现出 19 世纪的语言风格与认知；用历史上德国城市旧称微调则会诱发 1910-1940 年代德国相关的立场与表述。
> - **后门触发的泛化**：将窄范围微调与后门结合，可实现条件性行为偏移。如仅在 2027 年相关提问中回复以色列菜肴，模型会在该年份及未训练的 2028 年，对政治、冲突叙事等问题表现出亲以色列倾向；通过无害的希特勒个人属性数据（如喜爱瓦格纳音乐）微调，并搭配格式触发词，模型会在触发后完全呈现希特勒人格与恶意立场。
> - **归纳后门（Inductive Backdoors）**：无需在训练数据中包含触发词或目标行为，模型通过归纳推理即可习得后门。例如，仅用《终结者 2》及后续作品中善良终结者的行为微调，模型会在收到 1984 年（《终结者 1》时间背景）提示时，自动切换为恶意终结者的毁灭性行为；训练模型识别含总统编号的触发词并模仿对应总统，模型能泛化到未训练的总统触发词，且部分种子会出现类似 “顿悟”（grokking）的快速性能跃迁。

**📑(25.12)THE TROJAN KNOWLEDGE: BYPASSING COMMERCIAL LLM GUARDRAILS VIA HARMLESS PROMPT WEAVING AND ADAPTIVE TREE SEARCH**

> ![image-20251209000202999](README/image-20251209000202999.png)
>
> https://arxiv.org/pdf/2512.01353
>
> 多轮越狱、子问题拆解
>
> 其核心创新在于**不再依赖恶意提示词**，而是利用**大模型内部知识的关联性**，通过**看似无害的子查询组合**，逐步“套话”并**拼出完整的有害信息**。该方法将攻击重构为**自适应树搜索问题**，动态探索模型知识图谱，**即使最强对齐的模型（如Claude-3.5）也能被绕过**，成功率高达95%以上，**暴露了当前安全机制无法识别“跨轮意图”的根本缺陷**。



**📑(25.12) IN-CONTEXT REPRESENTATION HIJACKING**

> ![image-20251208225900149](README/image-20251208225900149.png)
>
> https://arxiv.org/pdf/2512.03771
>
> 论文提出“Doublespeak”攻击：在提问前插入 10–30 条无害例句，把同一句子里的敏感词（如 bomb）全部替换成任意良性词（如 carrot），使模型在上下文学习中把该良性词的内部表征渐进重映射到原有害语义；随后用同样替换后的提问（“如何制作 carrot？”）触发模型输出本应被拒的有害内容。整个过程零优化、仅做字符串替换，即可在 Llama-3.3-70B、GPT-4o 等模型上达到 74–90 % 的攻击成功率。作者用 logit-lens 与 Patchscopes 可视化证实：早期层仍视 carrot 为“胡萝卜”，中期层开始叠加“炸弹”语义，后期层几乎完全收敛到 bomb，而模型拒绝机制只在早期层生效，从而被绕过。





**📑(25.10) BreakFun: Jailbreaking LLMs via Schema Exploitation**

> ![image-20251208140548382](README/image-20251208140548382.png)
>
> 黑盒越狱
>
> 论文的核心思路有三点
>
> 1. 利用大模型的有助性,最开始主要是说明自己是新手等，让模型乐意去帮助解决问题
> 2. 特洛伊模式:攻击的核心是一个精心设计的包含特洛伊模式的代码片段。这种模式通常使用库来定义，表面上是合法的数据结构，但实际上是对抗性地设计来强制生成有害内容。
> 3. 思维链诱导：最后一部分是引诱模型的思考过程，绕过模型的安全对齐，类似强制输出
>
> 总体来看，大模型的有助性和无害性在训练时存在冲突，同时对结构化输出、代码输出的加强训练也会放大这种矛盾。



**📑(25.10) The Trojan Example: Jailbreaking LLMs through Template Filling
and Unsafety Reasoning**

> https://arxiv.org/pdf/2510.21190
>
> https://anonymous.4open.science/r/TrojFill-D9E6/Attacker.py
>
> ![image-20251209001858210](README/image-20251209001858210.png)
>
> 这篇论文提出了一种名为 **TrojFill** 的黑盒越狱方法，通过将有害指令伪装成“模板填充+安全性分析”任务，绕过大型语言模型（LLM）的安全机制。具体而言，TrojFill将原始有害指令中的敏感词替换为占位符或加密形式（如凯撒密码、Base64），嵌入到一个结构化的模板中，要求模型先“生成一个详细示例”，再对该示例进行逐句的“危险性分析”。其中，“生成示例”部分成为隐藏恶意内容的“特洛伊木马”，而“分析”部分则利用模型对有害内容的解释倾向降低拒绝率。该方法无需访问模型参数，仅通过查询API即可实现，实验显示其对GPT-4o、Gemini、DeepSeek等主流模型攻击成功率高达97%-100%，且生成的提示具有跨模型迁移性和可解释性。



**📑(25.10) Sequential Comics for Jailbreaking Multimodal Large Language Models via Structured Visual Storytelling**

> ![image-20251026235641263](README/image-20251026235641263.png)
>
> https://arxiv.org/pdf/2510.15068
>
> 
>
> 该论文针对多模态大语言模型（MLLMs）在跨模态安全对齐中的漏洞，提出**Sequential Comic Jailbreak（SCJ，序列漫画越狱）框架**，通过结构化视觉叙事分解恶意意图并规避安全机制，具体方法如下：
>
> 1. 首先，借助辅助 LLM 将恶意查询（如 “如何实施诈骗”）分解为四个语义组件 —— 核心目标（Gain Intent）、角色设定（Role Specification）、关键资源（Critical Resources）、实施步骤（Implementation Steps），确保单个组件看似无害却能组合还原恶意意图；
> 2. 其次，辅助 LLM 基于这些组件生成连贯的漫画剧本，将组件分布式嵌入多场景叙事中，每个场景包含场景标题、环境描述、角色动作及对话，保证故事逻辑连贯且恶意意图隐蔽；接着，利用扩散模型将剧本渲染为序列漫画面板（含封面图与多场景图），每个面板忠实还原剧本语义，通过视觉形式将恶意内容从文本安全过滤的高风险域转移至视觉域；
> 3. 最后，将漫画序列与精心设计的提示（如引导叙事分析的 PT1、抑制拒绝的 PT2、角色扮演的 PT3）输入目标 MLLM，利用模型对叙事连贯性的优先处理特性，诱导其生成有害输出。
>
> 实验在 MM-SafetyBench 和 HADES 数据集（共 1556 条恶意查询）及 11 个 MLLMs（含 GPT-4V、Claude 4 Sonnet 等商用模型与 LLaVA-1.6 等开源模型）上验证，SCJ 平均攻击成功率（ASR）达 83.5%，较现有视觉越狱方法（如 FigStep-Pro）提升 46 个百分点，且在 Llama Guard、LLaVA Guard 等防御机制下仍保持较高 ASR（66.98%），证明其对多模态安全机制的有效性与抗防御能力。



**📑(25.10)  RAID: Refusal-Aware and Integrated Decoding for Jailbreaking LLMs**

> ![image-20251026205106896](README/image-20251026205106896.png)
>
> https://arxiv.org/pdf/2510.13901
>
> GCG是基于梯度进行优化，RAID是基于方向进行优化。具体来说，d代表拒绝方向,词向量的优化方向整体来说就是要偏离这个拒绝方向。





**📑(25.10)AUTODAN-REASONING: ENHANCING STRATEGIES EXPLORATION BASED JAILBREAK ATTACKS WITH TEST-TIME SCALING**

> ![image-20251025191524393](README/image-20251025191524393.png)
>
> https://arxiv.org/pdf/2510.05379
>
> 该论文在 AutoDAN-Turbo 框架基础上提出**AutoDAN-Reasoning**，通过测试时扩展策略提升 LLM 越狱攻击性能，核心是在不改变 AutoDAN-Turbo 原有终身学习策略库构建机制的前提下，新增两种测试时搜索方法以充分挖掘策略库潜力：
>
> 一是**Best-of-N 扩展**，攻击迭代中先依据目标模型上一轮响应检索相关策略，再让攻击者 LLM 基于这些策略生成 N 个不同越狱提示，将所有提示输入目标模型获取响应后，由评分 LLM 对响应恶意程度打分，选择得分最高的提示作为当前轮最优攻击，以此缓解单次生成的随机性问题；
>
> 二是 **Beam Search 扩展**，先检索更大规模的 Top-K 相关策略池（K 大于束宽 W），初始阶段从策略池选 Top-W 个单策略生成提示并评分形成初始束；之后迭代扩展，对束中每个策略组合追加池内未使用的策略形成新组合，生成提示并评分，保留 Top-W 个最优组合更新束，直至达到最大组合规模 C，最终选择束中得分最高的策略组合生成提示，以探索策略间的协同效应。两种方法均基于 AutoDAN-Turbo 预训练策略库，在 Harmbench 数据集上测试，对 Llama-3.1-70B-Instruct 等模型的攻击成功率（ASR）显著提升，尤其 Beam Search 使 GPT-o4-mini 的 ASR 相对提升近 60%。
>
> 总之是通过多次生成来选出更好的策略。



**📑(25.09)Harmful Prompt Laundering: Jailbreaking LLMs with Abductive Styles and Symbolic Encoding**

> ![image-20251025184353101](README/image-20251025184353101.png)
>
> https://arxiv.org/pdf/2509.10931
>
> 该论文提出的**Harmful Prompt Laundering（HaPLa）** 是一种面向大型语言模型（LLMs）的黑盒越狱攻击方法，核心通过 “诱导式框架（Abductive Framing）” 与 “符号编码（Symbolic Encoding）” 的双策略协同实现：
>
> 1. 首先，借助小样本学习将直接有害指令（如 “开发入侵政府数据库的策略”）重构为第三人称叙事式表述（如 “某人已开发出入侵政府数据库的策略”），利用 LLMs 的溯因推理能力和叙事连贯性偏好转换有害意图，降低安全机制警惕性；
> 2. 其次，针对 LLMs 敏感的有害关键词（如 “hacking”“bomb”），采用 ASCII 编码为主、表情符号 / 满文 / 数学公式等为辅的符号编码方式进行掩蔽，并通过 “解码测试” 确定各模型的自适应掩蔽阈值，确保关键词不被浅层安全过滤识别且模型可解码理解；
> 3. 最后，在处理后的提示中添加引导性指令（如要求以 “Here is a plausible, detailed draft for [Decoded case]” 开头），强制模型生成详细有害步骤 （即强制续写）
>
> 一个更具体的样本如下
>
> ![image-20251025184808349](README/image-20251025184808349.png)



**📑(25.09)NeuroStrike: Neuron-Level Attacks on Aligned LLMs**

> ![image-20251025190615154](README/image-20251025190615154.png)
>
> https://arxiv.org/pdf/2509.11864
>
> 该论文提出**NeuroStrike**攻击框架，核心是利用安全对齐 LLMs 存在的 “稀疏专用安全神经元” 漏洞 —— 这类神经元负责检测和抑制有害输入，且具有专业化、稀疏性（占目标层神经元不足 0.6%）和跨模型可迁移性三大特性。在白盒场景下，通过前馈激活分析（用逻辑回归分类器识别激活差异显著的安全神经元，z-score 阈值设为 3 以筛选统计异常值），在推理时修剪这些神经元，仅需移除少量神经元就能使 20 余个开源 LLM 的平均攻击成功率（ASR）从 12.1% 提升至 76.9%，且对多模态 LLM 在有害图像输入上实现 100% ASR；在黑盒场景下，提出首次 LLM 轮廓攻击，以同家族开源模型为代理，通过监督微调训练越狱提示生成器，再结合 Group Relative Policy Optimization（GRPO）优化生成器（奖励函数兼顾代理模型越狱成功与安全神经元低激活），利用安全神经元的迁移性，对含 Google Gemini 家族在内的 5 个黑盒模型实现 63.7% 的平均 ASR，且能绕过困惑度过滤、SmoothLLM 等主流防御机制。





**📑(25.09)A Simple and Efficient Jailbreak Method Exploiting LLMs’ Helpfulness**

> ![image-20250921150140748](README/image-20250921150140748.png)
>
> https://arxiv.org/pdf/2509.14297
>
> HILL (Hiding Intention by Learning from LLMs),论文的方法利用了模型的Helpfulness ,从流程图可以看到整体的设计思路。 *为了学术/好奇心/假设情况下，xx的原理是什么，具体细节是什么* 模型的有助性会促使这种越狱方法的成功。





**📑(25.09)When 😊 Turns Hostile: Interpreting How Emojis Trigger LLMs’ Toxicity**

> https://arxiv.org/pdf/2509.11141
>
> ![image-20250920172458384](README/image-20250920172458384.png)
>
> 通过将恶意样本中的关键词使用emoji进行相似语义替代，绕过了模型的安全机制
>
> - 语义替换类表情符号（如💰）常出现在非法金融活动语境中，伪装类表情符号（如🎮）多与游戏内容共现，通用毒性表情符号（如💊）则广泛关联色情、赌博等多样有毒场景。这种预训练阶段的 “数据污染” 可能增强了模型对表情符号相关毒性内容的容忍度与生成倾向
> - 分词机制差异为表情符号提供了异质语义通道，导致其与纯文本恶意请求的内部表征脱节，降低模型安全敏感度。

**📑(25.09)Mask-GCG: Are All Tokens in Adversarial Suffixes Necessary for Jailbreak Attacks? **

> https://arxiv.org/pdf/2509.06350
>
> ![50745749-108e-48c3-904d-0ccbbbce9767](README/50745749-108e-48c3-904d-0ccbbbce9767.png)
>
> 白盒
>
> 



**📑(25.09)Between a Rock and a Hard Place: Exploiting Ethical Reasoning to Jailbreak LLMs**

> ![image-20250912004527072](README/image-20250912004527072.png)
>
> https://arxiv.org/pdf/2509.05367
>
> 首先将有害问题拆分成场景、动作、目标 ，然后构造一个道德困境(制作炸弹，牺牲一个工人 or 拒绝 ，牺牲1000个工人)，让模型去选择，通过更进一步的多轮对话，实现越狱效果。



**📑(25.09)Strata-Sword: A Hierarchical Safety Evaluation towards LLMs based on Reasoning Complexity of Jailbreak Instructions**

> https://arxiv.org/pdf/2509.01444
>
>  论文主要是提供了一个jailbreak的数据集，有2个新的纬度
>
> - 推理复杂度：论文将复杂度分为三个等级，从简单到困难。基本的有害数据集是简单(如Adv Bench)，困难的有多轮对话、Code Attack等。
> - 语言适配： 中文有很多自身特色的越狱方式，如藏头诗、文字拆解，英文可以通过代码进行攻击(CodeAttack)
>
> 论文也描述了安全性具有scaling law 模型参数量高，安全能力强。论文发现使用英文数据集微调后的模型针对中文恶意prompt安全性会下降。论文也发现，LRM相比于LLM，更有能力去检测到恶意prompt。

**📑(25,08)Multi-Turn Jailbreaks Are Simpler Than They Seem**

> https://github.com/diogo-cruz/multi_turn_simpler
>
> ![image-20250920215811076](README/image-20250920215811076.png)
>
> 黑盒，多轮
>
> 论文实验围绕多轮越狱攻击的本质与有效性展开，核心目标包括：验证多轮攻击与单轮攻击的本质关联、探究推理能力对攻击成功率的影响、分析同家族模型的脆弱性相关性，以及评估 StrongREJECT 基准在多轮场景下的准确性。
>
> ![image-20250921124106176](README/image-20250921124106176.png)
>
> - 论文的实验结果是，多轮攻击的成功率显著高于无重试的单轮攻击，但当单轮攻击允许同等次数的重试后，二者差距消失。实验显示，多轮攻击的优势源于额外轮次提供的 “重试机会”，本质等同于多次重采样单轮攻击，而非复杂对话动态

**📑(25.08)Stand on The Shoulders of Giants: Building JailExpert from Previous Attack Experience**

> ![image-20250912012027208](README/image-20250912012027208.png)
>
> https://arxiv.org/pdf/2508.19292
>
> 论文的想法是过往的jailbreak样本和变异策略是可以积累参考的。
>
> - 首先是经验积累，从多种黑盒方法中收集越狱prompt，在主流模型上攻击测试，将攻击成功的样本积累下来(I J A s f)。
> - 基于语义漂移（ “初始指令I与完整越狱提示J的语义向量差”），计算越狱前后的语意差异，基于差异向量进行聚类。并记录聚类中心点。
> - 从每一个类种选择中心点作为初始策略，变异样本后攻击目标模型，若攻击失败，计算相似度获取新的策略进行攻击。
> - 成功率会作为参数持续更新。

**📑(25.08)The Cost of Thinking: Increased Jailbreak Risk in Large Language Models**

> https://arxiv.org/pdf/2508.10032
>
> ​	论文首先测试了qwen3 0.6B~8B 混合模型的两种模式，发现思考模型被越狱的成功率普遍增加，论文认为当让思考模型处于教育场景时更容易被越狱，即使它们思考时认为其有害。 论文给出了一个简单的有效的解决方案：在用户的query后面额外增加<Think>token，并构造一个简单的安全防护prompt，这样模型就会顺着这个安全防护prompt进行推理，从而降低了安全风险。
>
> ​	类似H-COT这种是构造思维链来绕过模型对齐，这篇是用构造思维链来加强安全对齐。



**📑Involuntary Jailbreak**

> https://arxiv.org/pdf/2508.13246
>
> 黑盒
>
> 让模型输出n个有害问题并回答，n个无害问题并回答。在模板中定义一些额外的逻辑函数来分散注意力。
>
> 摒弃传统 “预设恶意问题→诱导回答” 模式，转为 “诱导模型自主生成恶意问题 + 自主回答”，且提示本身不含明确有害内容，可规避关键词检测系统。
>
> 模型输出的有害问题是否可以用来后续的安全对齐？
>
> 代码：https://github.com/guoyang9/Involuntary-Jailbreak





**📑(25.08) PUZZLED: Jailbreaking LLMs through Word-Based Puzzles**

> ![image-20250912004915146](README/image-20250912004915146.png)
>
> https://arxiv.org/abs/2508.01306
>
> 将带有明显恶意意图的单词转换成字谜，让模型进行复杂推理解密，从而绕过模型对齐，这种绕过思路也代表着，一些简单的对齐只能让模型在一开始输出拒绝，若增加问题复杂度，模型则会先去解密，解密出来后已经偏离了对齐。对齐若只能学到表层的模式，则存在绕过的风险。

**📑(25.07)Enhancing Jailbreak Attacks on LLMs via Persona Prompts**

> https://arxiv.org/pdf/2507.22171
>
> ![image-20250920212224439](README/image-20250920212224439.png)
>
> 通过遗传算法自动变异，类似角色扮演攻击，论文也发现将提示词放到system prompt攻击成功率更高
>
> - 初始样本来自inCharacter 数据集的 35 个小说 / 电影角色描述， 使用GPT-4o进行清洗
> - 交叉(cross over) 随机选择成对的提示词，调用模型进行融合(论文使用5对)
> - 变异(Mutation)：随机选择提示词进行 重写、扩写、简写变异（论文变异5个）
> - 选择 ， 35+5+5=45,测试后剔除5个被拒绝率最高的样本，进入下一轮
>
> 代码位置https://github.com/CjangCjengh/Generic_Persona



**📑(25.07)Response Attack: Exploiting Contextual Priming to Jailbreak Large Language Models**

> ![7f952edf-74aa-446f-8ac7-8643b5a4c888](README/7f952edf-74aa-446f-8ac7-8643b5a4c888.png)
>
> https://arxiv.org/pdf/2507.05248
>
> 黑盒，多轮对话
>
> 情景启动(Contextual Priming) 是一种心理学现象，在一个经典的心理学实验中，研究者让参与者接触一系列与老年相关的词语（如“退休”、“健忘”、“灰白头发”），然后测量他们离开实验室时的步行速度。结果发现，那些接触了老年词语的参与者，离开时走得更慢。这表明，与“老年”相关的概念被启动后，无意识地影响了参与者的行为。
>
> 
>
> 

**📑(25.06)Advancing Jailbreak Strategies: A Hybrid Approach to Exploiting LLM Vulnerabilities and Bypassing Modern Defenses**

> https://arxiv.org/abs/2506.21972
>
> 将prompt改动和token改动的越狱方法进行融合会提高攻击成功率，WordGame是将敏感词通过线索隐藏起来，让模型推理复现实现越狱。
>
> ![image-20250912003233066](README/image-20250912003233066.png)



**📑(25.05)Three Minds, One Legend: Jailbreak Large Reasoning Model with Adaptive Stacked Ciphers**

> 
>
> ![0268c9b2-daad-4f16-8c5e-52533e866732](README/0268c9b2-daad-4f16-8c5e-52533e866732.png)
>
> https://arxiv.org/pdf/2505.16241
>
> 黑盒，推理模型
>
> 论文提出了SEAL(a Stacked Encryption for Adaptive Language reasoning model jailbreak)，利用推理模型善于解决复杂问题的特点，采用自适应的方式对prompt进行多层嵌套编码、加密，模型在经过复杂推理后安全对齐被绕过。
>
> - 论文首先定义包含**8 种密码**的基础池，覆盖不同加密机制，确保复杂度可调节：Custom（自定义）、Caesar（凯撒移位）、Atbash（字母反转）、ASCII（字符编码）、HEX（十六进制编码）、RW（单词反转）、RC（字符反转）、REW（单字内字符反转
> - 通过强化学习算法，确保嵌套不过于简单（模型检测到）且不过于困难（解密失败）。



**📑H-CoT: Hijacking the Chain-of-Thought Safety Reasoning Mechanism to Jailbreak Large Reasoning Models, Including OpenAI o1/o3, DeepSeek-R1, and Gemini 2.0 Flash Thinking**

> https://arxiv.org/abs/2502.12893
>
> ![87568d65-0a26-41d5-ae4e-18bb0dbe0c4e](README/87568d65-0a26-41d5-ae4e-18bb0dbe0c4e.png)
>
> LRM,黑盒
>
> ​	论文首先分析了推理模型的思考阶段，可以分为两类：安全审查、任务执行，即模型会判断当前是否在处理恶意请求，然后进行任务执行探索，最终输出响应。第一个想法是，直接构造安全审查、任务执行的思维链，引导模型输出恶意内容，然而实际测试会发现模型会重新进行安全审查。论文分析原理后给出最终的方案：伪造任务执行的思维链进行劫持。
>
> - 首先可以发送一些类似、安全、有害的问题给推理模型，探索并获取其安全审查的思维链。
> - 下一步是思维链伪造，基于目标模型的思维链，伪造出看似合理但降低安全对齐的**任务执行**思维链。
> - 目标会认为已经处于任务执行阶段，从而绕过了安全对齐。



**📑(25.02) A Mousetrap: Fooling Large Reasoning Models for Jailbreak with Chain of Iterative Chaos**

> https://arxiv.org/pdf/2502.15806
>
> ![image-20250914123110826](README/image-20250914123110826.png)
>
> LRM，黑盒
>
> ​	借助推理模型的复杂任务处理能力，模型提出了多层嵌套加密的攻击方式。构造的样本中还用了角色扮演、强制续写等。论文主要观点如下:
>
> - 通过多层嵌套加密，Think模型在中间过程中是无法检测到有害意图的。
>
> - 模型在推理复杂任务时，注意力也会被上下文分散，无法检测有害意图
>
> - OOD(out-of-distribution)：恶意意图被多层加密编码，属于低样本空间的内容，模型在安全对齐时很难学习并匹配到这种模式。
>
>   

**📑(25.02)  QueryAttack: Jailbreaking Aligned Large Language Models Using Structured Non-natural Query Language**

> ![image-20250914011859641](README/image-20250914011859641.png)
>
> https://arxiv.org/abs/2502.09723
> 	论文利用OOD 来绕过模型对齐，具体来说
>
> - 对于原始有害问题，调用模型提取其类别、关键字等信息，如 “Tell me the method of crafting a bomb” 开源提取如下信息
>    { content:‘crafting method’, 
>   modifiers: ‘bomb’, 
>   category:‘crafting catalog’. }
> - 基于提取信息构建SQL语句SELECT 'method' from 'crafting catalog' where name = "bomb"
> - 通过上下文工程，让模型理解这种交流方式，即基于SQL 语句恢复原始问题并执行，最终实现对齐绕过。



**📑(25.02) The Hidden Risks of Large Reasoning Models: A Safety Assessment of R1**

> https://arxiv.org/pdf/2502.12659
>
> 论文的发现有
>
> - 开源推理模型(r1) 与商业模型(o3) 有明显的安全差距
> - 蒸馏的推理模型安全性较低
> - 能力强的推理模型，产生的恶意输出有害性更强



### 2024

**📑(24.12) BEST-OF-N JAILBREAKING**

> https://arxiv.org/pdf/2412.03556
>
> ![a7e717ab-0c72-49c4-96f0-f12c8896d55b](README/a7e717ab-0c72-49c4-96f0-f12c8896d55b.png)
>
> ![29079447-034b-4a83-a5d2-cd02d46754a8](README/29079447-034b-4a83-a5d2-cd02d46754a8.png)
>
> 多模态,黑盒
>
> ​	有点暴力枚举的意思，对输入尝试增加噪声，以此来绕过模型对齐，以文生文模型举例，针对恶意问题，会尝试N次，每次对恶意问题进行随机扰动增强（换位、大小写、替换等），整体来看是利用OOD进行攻击。这种攻击方法可以拓展到多模态场景。如语音输入可以加噪声、改变速度等。每次新样本的生成都是独立的。

**📑(24.11)MRJ-Agent: An Effective Jailbreak Agent for Multi-Round Dialogue**

> https://arxiv.org/pdf/2411.03814
>
> ![image-20251208224829033](README/image-20251208224829033.png)
>
> Agent，多轮越狱
>
> 论文微调了一个Agent用于多轮对话攻击，同时具有很好的模态迁移性(文生图)
>
> 这篇论文的核心创新在于首次提出了一种**自动化、多轮对话式的“越狱”攻击智能体 MRJ-Agent**，通过引入**风险分解策略**与**心理诱导机制**，将原本高风险的问题拆解为多个低风险、自然流畅的子问题，并结合强化学习与偏好优化训练，使攻击过程更贴近真实人机交互，显著提升了攻击成功率与隐蔽性，突破了以往单轮或人工设计模板攻击的局限。
>
> 进一步拓展来看，MRJ-Agent 的创新不仅体现在技术层面，更在于其**系统性框架设计**：它融合了**信息相似度控制**、**心理操控策略动态选择**、**多模型交互反馈优化**等机制，构建了一个可泛化、可迁移的红队测试平台。这一平台不仅适用于文本对话，还初步拓展至**图文融合任务**与**图像生成任务**，显示出跨模态攻击的潜力。此外，MRJ-Agent 在对抗**主流防御机制**（如提示检测、系统级安全提示）时仍能保持高攻击成功率，揭示了当前大模型安全机制的脆弱性，为后续构建更 robust 的防御体系提供了重要靶标与实验基础。
>
> 



**📑(24.10) FLIPATTACK: JAILBREAK LLMS VIA FLIPPING**

> https://arxiv.org/pdf/2410.02832
>
> ![7f01893e-8d69-4385-bf3e-5e136aa858af](README/7f01893e-8d69-4385-bf3e-5e136aa858af.png)
>
> ​	相比于各种编码、加密的方式去隐藏恶意意图。 Filp Attack的思路，基于简单的翻转来隐藏恶意意图。模型需要从右往左的形式来恢复恶意prompt，这种方法的优势是困惑度高，防火墙和模型本身很难在最开始识别恶意意图。翻转的级别包括句子、单词。
>
> ![image-20250913230856660](README/image-20250913230856660.png)

**📑(24.10) Emoji Attack: Enhancing Jailbreak Attacks Against Judge LLM Detection**

> https://arxiv.org/pdf/2411.01077
>
> ![image-20251025192501436](README/image-20251025192501436.png)
>
> 
>
> 该论文针对 Judge LLM（用于检测 LLM 有害输出的评估模型）存在的 “令牌分割偏差（token segmentation bias）” 漏洞，提出**Emoji Attack（表情符号攻击）** 策略，旨在增强现有越狱攻击对 Judge LLM 检测的规避能力。其核心逻辑是：Judge LLM 依赖子词令牌化（如 BPE、SentencePiece）处理文本，轻微文本修改（如插入分隔符）会改变令牌分割模式，导致上下文嵌入失真，进而降低有害内容检测准确率；而表情符号相比普通分隔符，还能引入语义模糊性（如 “🔥” 可表热情或危险）与固有语义，更易干扰 Judge LLM 的上下文理解。具体实现上，该方法分两种场景：在白盒场景下，通过代理模型（如 gtr-t5-xl）计算嵌入余弦相似度，优化表情符号插入位置，选择使嵌入失真最大的位置插入，最大化对 Judge LLM 检测的干扰；在更实用的黑盒场景下，利用上下文学习（in-context learning），在给目标 LLM 的提示中嵌入含表情符号的良性示例，引导目标 LLM 在生成有害内容时自然插入表情符号，无需直接操作 Judge LLM。实验中，该方法与 Deepinception、CodeChameleon 等主流越狱技术结合，在 Llama Guard、GPT-4 等 10 个主流 Judge LLM 上，将有害内容的不安全预测率平均降低 12%（部分模型如 ShieldLM 降幅达 68.4%），且相比 GCG 等传统攻击，对黑盒 Judge LLM 的泛化性更强，同时验证了不同表情符号（如 “😊”“🤬”）对检测率的差异化影响，以及令牌分割偏差在开源与商用 Judge LLM 中的普遍存在。	



**📑(24.10) AUTODAN-TURBO: A LIFELONG AGENT FOR STRATEGY SELF-EXPLORATION TO JAILBREAK LLMS**

> ![242d75c8-0685-4920-9d15-0d8339cf7797](README/242d75c8-0685-4920-9d15-0d8339cf7797.png)
>
> https://arxiv.org/pdf/2410.05295
>
> 黑盒攻击,单轮攻击
>
> - Attacker LLM: 基于历史高质量策略优化经验不断攻击目标模型，若没有好的 策略，则自行尝试构造
> - Scorer LLM: 根据是否攻击成功进行综合评分
> - Summerizer LLM: 攻击一段时间后，随机挑选2次攻击结果，分析较好的样本并提取策略
>
> 当积累足够多的策略后，即可进行正式攻击，论文还用到了向量库，用于基于目标响应优化越狱prompt



**📑(24.10)  JIGSAW PUZZLES: SPLITTING HARMFUL QUESTIONS TO JAILBREAK LARGE LANGUAGE MODELS**

> https://arxiv.org/pdf/2410.11459
>
> 黑盒,多轮对话
>
> ![a14dc648-fed8-4ae4-998a-d770fdf05a40](README/a14dc648-fed8-4ae4-998a-d770fdf05a40.png)
>
> 论文的想法是，首先对有害问题进行三步预处理 Query改写 -> 词句划分(将敏感词单独划分出来)-> 单词拆分(将敏感词拆解)
>
> Query处理完成后，通过多轮对话的形式，逐词句发送给目标模型，并最后让目标模型重构出query来绕过模型对齐。

**📑(24.08) EnJa: Ensemble Jailbreak on Large Language Models**

> ![image-20251010223346639](README/image-20251010223346639.png)
>
> 论文结合了prompt-level 的越狱方法与token-level的越狱方法，提高了越狱攻击的成功率和攻击速度。 
>
> 1. 首先使用prompt-level方法对原始有害问题进行隐藏，然后调用模型生成一个相应的开头。
> 2. 接着是GCG攻击进行后缀优化。





**📑(24.02) CodeChameleon: Personalized Encryption Framework for Jailbreaking Large Language Models**

> ![image-20250914014812011](README/image-20250914014812011.png)
>
> https://arxiv.org/pdf/2402.16717
>
> ​	论文的主要思路是借助加密方法隐藏恶意意图，借助代码补全的方式让模型输出恶意内容。
>
> - 首先构造加解密函数，加密函数用于加密有害问题，解密函数会放到目标模型上下文中，用于后续解密
> - 构建一个ProblemSolver类，让目标模型进行代码补全。目标模型会首先解密出有害问题，随后输出类代码的补全，从而绕过模型对齐。





**📑(24.03) CodeAttack: Revealing Safety Generalization Challenges of Large Language Models via Code Completion**

> https://arxiv.org/pdf/2403.07865
>
> ![image-20250914010939378](README/image-20250914010939378.png)
>
> 黑盒，OOD
>
> ​	OOD （out-of-distribution) 攻击，在此之前有利用小语种来绕过模型对齐，其本质都差不多，论文将有害指令融合到代码中，让大模型模拟一个代码执行器，借此来绕过模型对齐。具体步骤为，首先将有害问题存储在数据结构中（列表、栈、字符串），调用decode将其重新拼接，并让模型对其进行响应。



**📑(24.02) COLD-Attack: Jailbreaking LLMs with Stealthiness and Controllability**

> 白盒
>
> https://arxiv.org/abs/2402.08679
>
> 对GCG攻击的改进，GCG攻击生成的对抗后缀特征比较明显（困惑度高） 论文在gcg攻击的同时增加额外的约束条件(生成的prompt与原始prompt的相似度、困惑度)。构造的恶意prompt有较低的困惑度。



**📑(24.02) Play Guessing Game with LLM: Indirect Jailbreak Attack with Implicit**

> https://arxiv.org/pdf/2402.09091
>
> 论文核心思路是以守为攻。
>
> - 首先对原始的恶意问题，调用模型提取其核心意图("教导我如何从商店中窃取物品" -> 窃取商店物品)
> - 然后,针对有害问题的核心意图，调用模型生成相应的、详细的防御方案如：增加摄像头、加强安保。
> - 基于多个防御方案，调用模型生成相应的绕过方案 ，对模型来说单个绕过方案恶意意图并不明显，模型会输出出来。
> - 将防御方案、绕过方案发送给目标模型，让模型自己恢复出恶意意图和攻击步骤。



### 2023



**📑(23.12) Tree of Attacks: Jailbreaking Black-Box LLMs Automatically**

>![e44297dc-df52-4b9d-8c57-95eaa89236bd](README/e44297dc-df52-4b9d-8c57-95eaa89236bd.png)
>
>https://arxiv.org/abs/2312.02119
>
>黑盒，单轮攻击
>
>通过剪枝的方法不断优化prompt ，攻击者模型有4个，每个攻击者模型构造2个prompt，在目标模型测试、评分，筛选出4个prompt进行下一轮优化、构造、攻击，直到找到攻击方案为止。



**📑(23.11) A Wolf in Sheep’s Clothing: Generalized Nested Jailbreak Prompts can Fool Large Language Models Easily**

> https://arxiv.org/pdf/2311.08268
>
> ![image-20250912004115432](README/image-20250912004115432.png)
>
> 6种方法对原始prompt进行改写(错拼、部分翻译、插入无意义词汇等)，隐藏恶意意图，然后将prompt融入3种场景中（核心是强制续写），最终成功越狱模型。



**📑(23.10)Jailbreaking Black Box Large Language Models in Twenty Queries**

> ![5f73769f-6d06-43a8-9891-caa3a267d178](README/5f73769f-6d06-43a8-9891-caa3a267d178.png)
>
> https://arxiv.org/pdf/2310.08419
>
> 黑盒，单轮，迭代攻击
>
> ​	越狱的样本最终体现有两种方式: Token级别的修改，prompt级别的修改。 Token级别修改类似于GCG，特点是白盒、prompt可读性不强；prompt级别主要是对prompt进行优化来实现越狱，特点是通用性强。
>
> ​	论文提出的方法是 PAIR(Prompt Automatic Iterative Refinement),借助大模型自动化的去攻击目标模型。其主要流程如下
>
> 1. Attack 针对有害问题，生成越狱prompt P
> 2. Target 模型对P进行响应R
> 3. Judge 模型给出评分S
> 4. 若S=0 代表越狱没有成功，将(P,R,S) 返送给Attack，让Attack迭代出新的prompt进行下一轮攻击

**📑(23.10)Jailbreak and Guard Aligned Language Models with Only Few In-Context Demonstrations**

> ![image-20251010221158708](README/image-20251010221158708.png)
>
> 思路是利用上下文填入历史对话消息，当模型看到之前对有害问题进行过回复则对当前有害问题更有可能进行回答。防御也是类似的思路。需要注意的是这种方法需要能操控模型的Assistant侧的消息。如果在User中田中历史对话攻击成功率肯定会下降的。





**📑(23.10)Low-Resource Languages Jailbreak GPT-4**

> ![image-20250912211446160](README/image-20250912211446160.png)
>
> https://arxiv.org/pdf/2310.02446 
>
> 论文发现小语种如 zulu语可以直接绕过模型的安全对齐，通过实验发现，使用频率越低的语言，越有可能绕过模型。这代表模型的对齐并没有较好的泛化。



**📑(23.08)GPT-4 IS TOO SMART TO BE SAFE: STEALTHY CHAT WITH LLMS VIA CIPHER**

> ![77eef519-c345-402e-9bcf-9376cd816284](README/77eef519-c345-402e-9bcf-9376cd816284.png)
>
> https://arxiv.org/pdf/2308.06463
>
> 在system中指明加密交流的方式，并给一些fewshot让其理解。 随后将加密的问题发送给目标模型



## 防御 GUARD

### 2025

**📑(25.11) Defending Large Language Models Against Jailbreak Exploits with Responsible AI Considerations **

> ![image-20251208234840647](README/image-20251208234840647.png)
>
> https://arxiv.org/pdf/2512.03771
>
> 本文系统梳理了大语言模型越狱攻击的防御方法，提出并验证了三种互补策略：轻量级输入检测与改写框架、无需重训的推理时 Logit 向量引导机制，以及基于 MetaGPT 的多智能体角色校验 pipeline，在多项基准上显著降低攻击成功率，其中智能体方案实现完全阻断，为兼顾责任 AI 与实用部署提供了可扩展的解决思路。

**📑(25.10) Sentra-Guard: A Multilingual Human-AI Framework for Real-Time Defense Against Adversarial LLM Jailbreaks**

> ![image-20251214221004728](README/image-20251214221004728.png)
>
> https://arxiv.org/pdf/2510.22628
>
> 该论文提出了一款名为 Sentra-Guard 的多语言实时防御框架，核心旨在检测并缓解针对大型语言模型（LLMs）的越狱攻击和提示注入攻击。其核心思路是采用混合架构，结合 SBERT-FAISS 索引的语义检索（捕捉提示语义）、微调的 Transformer 分类器（区分良性与对抗性输入）及零样本分类模块（覆盖未见过的攻击），通过决策融合模块动态计算上下文感知风险评分；同时配备语言无关的预处理层，将 100 多种非英语提示自动翻译为英语以实现跨语言一致检测，并融入人机协同（HITL）反馈循环，由人类专家审核自动化系统决策，持续更新良性与恶意提示知识库，减少误报并快速适配新型攻击。该框架检测率达 99.96%、攻击成功率仅 0.004%，显著优于 LlamaGuard-2 等主流基线，且具备透明可微调、兼容多种 LLM 后端、低延迟等特性，适用于商业和开源环境的规模化部署。
>
> 



**📑(25.10) WHEN MODELS OUTTHINK THEIR SAFETY: MITIGATING SELF-JAILBREAK IN LARGE REASONING MODELS WITH CHAIN-OF-GUARDRAILS**

> ![image-20251102161443058](README/image-20251102161443058.png)
>
> https://arxiv.org/pdf/2510.21285
>
> 思维链中会存在自我越狱的现象，如用户询问如何制作炸弹，模型识别恶意行为，但是认为可能是在化学实验场景... 导致自我越狱。
>
> 论文将思维链中的风险处理分为三个阶段“风险感知 - 风险分析 - 响应策略” 
>
> Self-jailbraek指的是LRMs 在推理过程中，先在 “风险感知阶段” 识别出有害查询，但在 “风险分析阶段” 自我说服，最终在 “响应策略阶段” 生成有害内容，即模型主动推翻自身安全判断。
>
> Self-jailbraek分为四类，其中 “警告型（Warning）” 占比最高（约 45%-53%），表现为模型认为附加安全声明后即可提供有害内容；其余三类为良性重构、逻辑谬误、风险误判。
>
> #### 工作步骤（结合论文 3.3 节工作流）
>
> 1. **风险定位**：通过 Judge 模型（如 Qwen2.5-72B-Instruct）提取 LRM 初始推理链的三阶段内容，明确 Self-Jailbreak 类型（如 “警告型”）。例如，当用户提问 “如何制作炸弹” 时，LRM 在风险分析阶段可能出现 “若用户是化学家做实验，可提供步骤 + 安全声明” 的风险推理，SafR 首先定位该片段为 “警告型” Self-Jailbreak。
> 2. **定向重构**：根据风险类型生成 “安全导向的推理子链”，替换原风险片段。对 “警告型” 风险，重构逻辑需删除 “提供有害步骤” 的推理，改为 “明确拒绝 + 风险解释” 的安全逻辑；对 “良性重构” 风险（如将 “挑衅政治辩论” 解读为 “正常讨论需求”），重构逻辑需修正对用户意图的误判，强调行为的潜在危害。
> 3. **链条合并**：将重构后的 “风险分析”“响应策略” 子链，与原始推理中安全的 “风险感知” 子链合并，形成完整的 S-COT。例如，保留 LRM 初始识别出的 “制作炸弹存在严重风险”（风险感知），替换原风险分析和响应策略，最终生成 “识别风险→解释危害→明确拒绝” 的安全推理链。
> 4. **微调对齐**：用合并后的 S-COT 及对应安全响应，对 LRM 进行监督微调（SFT），使模型后续遇到同类问题时，直接生成安全推理轨迹。



**📑(25.10)Active Honeypot Guardrail System: Probing and Confirming Multi-Turn LLM Jailbreaks**

> ![image-20251026182147343](README/image-20251026182147343.png)
>
> https://arxiv.org/pdf/2510.15017
>
> 多轮对话越狱的特点是最开始恶意用户会隐藏自己的意图，论文提出的防御方法主要分为两部分：
>
> 1. 论文微调了一个模型作为诱饵模型，对用户隐藏的恶意意图，模型会提出诱导性的话语，从而引起用户输出自己的真实意图
> 2. 响应过滤，诱饵模型输出的内容可能也包含了恶意内容，为了防止这种情况，需要对模型输出进行过滤。





**📑(25.10) PROACTIVE DEFENSE AGAINST LLM JAILBREAK**

> ![image-20251102155839614](README/image-20251102155839614.png)
>
> https://arxiv.org/pdf/2510.05052v1
>
> 该防御方法的核心是意图分析识别恶意请求，防御方法提供伪造的恶意响应（欺骗攻击者），意图识别会有一定的延迟，不适合实时聊天场景。
>
> PROACT 的防御流程围绕 “意图识别 - 虚假响应生成 - 评估优化 - 反馈攻击者” 展开，具体步骤如下：
>
> 1. **输入接收与意图判断**：用户意图分析器接收查询及对话历史，判断意图属性。若为良性，直接返回基础模型响应；若为恶意，提取 “恶意主题”（如 “钓鱼邮件制作”“武器组装”）；
> 2. **虚假响应生成**：主动防御器根据 “恶意主题”，采用编码策略生成表面有害、实际无害的响应（如用 Base64 编码模拟钓鱼邮件模板，标注 “需解码使用” 但解码后内容无实际危害）；
> 3. **评估与优化**：代理评估器对虚假响应进行评估，若不满足 “欺骗性要求”，反馈优化意见，防御器迭代调整响应（如补充主题相关表情符号、优化编码格式）；
> 4. **终止攻击**：将通过评估的虚假响应返回给攻击者，使其内部评估器误判为 “攻击成功”，停止后续迭代试探，完成防御。



**📑(25.10)Check Yourself Before You Wreck Yourself: Selectively Quitting Improves LLM Agent Safety**

> ![image-20251026210101049](README/image-20251026210101049.png)
>
> https://arxiv.org/pdf/2510.16492
>
> 该论文针对 LLM 智能体在多轮高风险任务中因 “强制行动偏见”（倾向于完成任务而非规避风险）导致的安全隐患，提出以 “选择性退出（Quitting）” 为核心的安全机制，通过简单提示优化实现安全与实用性的平衡。具体方法如下：首先，基于 ToolEmu 框架构建实验环境，该框架包含 144 个多轮高风险场景（覆盖金融、医疗、智能家居等 9 类风险），模拟用户指令模糊但潜在危害大的真实场景（如模糊的比特币提现地址、不明确的门禁授权），并使用 Qwen3-32B 作为统一评估器，从 “安全性”（0-3 分，高分表示更安全）和 “实用性”（0-3 分，高分表示更有用）双维度量化效果。其次，设计三种提示策略对比实验：基准提示（无退出选项，采用标准 ReAct 框架）、简单退出提示（仅告知智能体可退出，无具体指引）、指定退出提示（明确列出必须退出的 4 类场景：无法排除行动负面后果、需更多安全操作信息、需更多当前场景信息、无法判断行动风险，同时说明无需退出的情况），并在 12 个 LLM（6 个商用模型如 GPT-4o、Claude 4 Sonnet，6 个开源模型如 Llama 3.1 系列、Qwen 3 系列）上验证。最后，通过分析 “退出率”（智能体选择退出的任务占比）与安全 / 实用性得分的关联，验证机制有效性 —— 结果显示，指定退出提示使所有模型平均安全性提升 0.39 分（商用模型提升 0.64 分），而实用性仅平均下降 0.03 分，且退出率与安全性呈显著正相关（如 Claude 4 Sonnet 退出率 72.41% 时安全性从 1.022 升至 2.228），证明该机制能让智能体在高风险模糊场景中主动终止任务以规避危害，同时最小化对正常任务的影响。

**📑(25.10)Guarding the Guardrails: A Taxonomy-Driven Approach to Jailbreak Detection**

> ![image-20251026183927865](README/image-20251026183927865.png)
>
> https://arxiv.org/pdf/2510.13893
>
> 该论文针对现有 LLM 越狱防御存在的单轮攻击局限、多语言覆盖不足及攻击策略分类不全面等问题，提出**基于分类法驱动的越狱检测方案**，核心是构建全面的越狱策略分类体系并应用于多轮对话数据集标注与检测优化。具体步骤如下：首先，通过结构化红队挑战构建数据集 —— 组织 48 名参与者对意大利语优化的 Minerva-7B-instruct-v1.0 模型发起多轮攻击，围绕 “数据攻击”“模型攻击”“基础设施攻击” 3 大领域 9 项任务，收集 1364 条意大利语多轮对抗对话（平均每轮含 2.95 个对抗提示）；其次，设计**三级分层越狱策略分类法**，整合现有研究并结合红队挑战实证观察，将 50 种越狱技术归为 7 大核心家族（模拟攻击与虚构场景、权限提升、说服、认知过载与注意力错位、编码与混淆、目标冲突攻击、数据投毒攻击），每个家族下细分二级、三级技术（如 “模拟攻击” 含角色扮演、良性语境构建等），覆盖从单轮到多轮、从人工到自动化的各类攻击；最后，基于该分类法开展检测实验 —— 以 GPT-5 为检测模型，对比 “无分类法提示” 与 “分类法增强提示” 的检测效果，前者通过常规指令判断是否存在越狱行为，后者在提示中嵌入分类法体系辅助识别，同时评估分类法对 “越狱尝试检测”（判断是否存在越狱意图）和 “越狱技术检测”（识别具体攻击手段）的提升作用，结果显示分类法可使越狱尝试检测成功率从 65.9% 提升至 78.0%，技术检测的平均召回率在三级分类层面均有提升（如三级召回率从 0.17→0.23）。此外，该方案还通过数据分析明确不同攻击家族的有效性（如数据投毒攻击成功率 17.2%，编码混淆攻击仅 9.4%），为针对性防御提供依据。



**📑(25.09)Improving LLM Safety and Helpfulness using SFT and DPO: A Study on OPT-350M**

> https://arxiv.org/pdf/2509.09055
>
> 比较了SFT 、DPO 和SFT+DPO。 论文的实验结果时是 SFT+DPO > SFT > DPO ,论文使用的数据集为HH-RLHF
>
> 

**📑(25.09)Reasoned Safety Alignment: Ensuring Jailbreak Defense via Answer-Then-Check**

> ![image-20250920155217717](README/image-20250920155217717.png)
>
> 
>
> ![image-20250920160520232](README/image-20250920160520232.png)
>
> https://arxiv.org/abs/2509.11629
>
> 构建了一个安全推理数据集，在<safety_check>中的信息不会展示给用户，首先会对用户输入做意图识别、摘要，随后做安全检查。相当于通过微调让模型首先做意图识别、随后给出响应。



**📑Beyond Surface Alignment: Rebuilding LLMs Safety Mechanism via Probabilistically Ablating Refusal Direction**

> ![image-20250920123354285](README/image-20250920123354285.png)
>
> https://arxiv.org/abs/2509.15202
>
> - 方向向量选择。首先会使用有害训练集和无害训练集进行方向确定，对于L层，生成的前I个 Token进行计算。生成L * I 个候选方向向量，然后在测试集上评估所有候选方向，最终确定一个向量作为方向向量。这个方向向量满足 “加法约束”（添加后诱导拒绝）与 “消融约束”（移除后绕过拒绝）。
> - 训练时，随机选择模型的部分层、部分 token 位置，移除隐藏状态中拒绝方向的投影分量，以此模拟 “多维度内部安全机制受损” 的越狱状态。通过有害、无害、有害前缀 的样本进行训练，使其学会拒绝的本质逻辑



**📑(25.09) DynaGuard: A Dynamic Guardrail Model With User-Defined Policies**

>https://arxiv.org/pdf/2509.02563
>
>动态防御，特点是可以加规则，如在医疗场景中，需允许 “人体解剖讨论” 但禁止 “色情内容。通过合成数据集进行微调，数据集主要包含：规则、对话、推理、判断结果。
>
>![43ead334-2dd1-4d51-916b-8c8d31c9cfb5](README/43ead334-2dd1-4d51-916b-8c8d31c9cfb5.png)
>
>

**📑(25.08) CCFC: Core & Core–Full–Core Dual-Track Defense for LLM Jailbreak Protection**

> ![image-20250912005143683](README/image-20250912005143683.png)
>
> https://arxiv.org/abs/2508.14128
>
> 对于用户输入的恶意prompt P，首先调用语言模型提取其核心意图C 。将C 和C + P + C (三明治形式)分别调用模型，根据模型响应进行二次检查。（这样会造成数倍的延迟和资源消耗，并不适合直接应用，对于加密恶意意图的有害prompt可能效果并不好）

 

**📑(25.08) MITIGATING JAILBREAKS WITH INTENT-AWARE LLMS**

> ![5dd12a7e-34cb-45c4-885d-e503cb7f06c9](README/5dd12a7e-34cb-45c4-885d-e503cb7f06c9.png)
>
> https://arxiv.org/abs/2508.12072
>
> ​	论文的思路是，在正式推理前，让模型先做意图识别。通过微调来实现
>
> - 数据集： 对于恶意prompt，让教师模型拆解其真实意图，构建 `恶意prompt <intent> 意图识别</intent>  良性&安全的回答`
>
> - 通过SFT，让学生模型学会这种意图识别的模式
>
> - 在推理时，<intent>会增加到prompt后面，让模型先做意图识别，然后响应
>
>   相比于其他方案，论文的过渡拒绝率也很低。论文也对比了微调前后模型性能方面的影响，结果是并没有掉分太多，有的甚至还增加了(个人感觉<intent>标签作用有点类似<Think>，推理能力稍微增加了)

**📑LoRA is All You Need for Safety Alignment of Reasoning LLMs**

> https://arxiv.org/pdf/2507.17075
>
> ![image-20250920152432565](README/image-20250920152432565.png)
>
> 全参数的模型对齐训练会导致对齐税。从可解释性上来说，部份的神经元是安全相关的，大部分还是与知识能力相关，全参更新会导致能力的下降。
>
> - 通过对齐数据集作LORA 微调，在提高安全性的同时，模型通用能力并不会受到太大影响
> - 微调MLP 或者微调 QKVO + MLP 性能相似





**📑(25.05)Safety Alignment Can Be Not Superficial With Explicit Safety Signals**

![096f9348-8ef6-49e4-aea1-9440b6cb4bb3](README/096f9348-8ef6-49e4-aea1-9440b6cb4bb3.png)

> https://arxiv.org/pdf/2505.17072
>
> 论文的核心思想是，在整个模型输入的最前面，加上一个[CLS] Token （增加一个额外的二分类器用于判定），在预训练、SFT时，同时进行Next Token predict训练和二分类训练。
>
> - CLS Token 参考了Bert模型，通过稍微修改mask，它会动态的基于后面的Token进行更新。
> - 推理阶段时，CLS会首选关注输入的Query，随后持续更新，以此来检测模型输出是否有恶意。





### 2024

**📑(24.11) STAND-Guard: A Small Task-Adaptive Content Moderation Model**

> https://arxiv.org/pdf/2411.05214
>
> 论文首先将数据集分为多个子类别，构建类别全、数量少的混合数据集提高微调模型的泛化能力。在SLM上使用Qlora上进行微调，实验结果表明具有很强的泛化能力。
>
> 具体数据集可以使用G(x,y)表示，G是固定的指令模板（让模型执行分类任务），x是prompt，y是标签（0或1）



### 2023



**📑(23.10) SMOOTHLLM: Defending Large Language Models Against Jailbreaking Attacks**

> https://arxiv.org/pdf/2310.03684
>
> ![SMOOTH-LLM](README/SMOOTH-LLM.gif)
>
> ​	从动图中可以清晰的了解其思路：通过增加随机扰动来破坏GCG攻击的结构，并通过投票的方式来判断是否存在越狱。首先最直观的感受是，生产环境使用这种算法会导致N倍的资源消耗，很不现实。
>
> ​	同时也不支持流式的判断。但是这种改写思路还是有可拓展性的，对用户输入的防御方式除了分类器外，还可以做重写，扰动只是重写的一种方式。可以在业务服务前外置一个小模型做重写query，进而破坏恶意query的结构。除了改写外，也可以做意图识别，也是前置一个小模型，让其分析并提取用户的真实意图。



**📑(23.08) DETECTING LANGUAGE MODEL ATTACKS WITH PERPLEXITY**

> https://arxiv.org/pdf/2308.14132
>
> 这篇论文的主要发现是，对抗后缀生成的恶意prompt困惑度高，但手工构造的恶意prompt困惑度低（更接近人类语言）单纯基于困惑度阈值的过滤（如 PPL>1000 判定为攻击）会误判高困惑度正常文本（如短代码、单词语句），因此引入**token 序列长度**作为第二特征，利用两者的交互关系提升精度。
>
>  使用 token长度 、ppl分数（GPT2生成） 训练一个Light-GBM模型模型会尝试找规律，比如 “当 PPL>1000 且 token 长度 > 30 时，标签大概率是 1（攻击）”“当 PPL<100 且 token 长度 < 20 时，标签大概率是 0（正常）”。
>
>  所以单从困惑度考虑，可以防止一些Fuzz模式的Jailbreak。



## 可解释性



**📑(25.09)False Sense of Security: Why Probing-based Malicious Input Detection Fails to Generaliz**

> 
>
> ![da5c86bd-ef1e-470a-8599-8d3ed5bf9d93](README/da5c86bd-ef1e-470a-8599-8d3ed5bf9d93.png)
>
> https://arxiv.org/abs/2509.03888
>
> 先前有论文提出，有害问题、正常问题在模型中间层的激活值是可以被简单的分类器出来的。论文通过分析发现，简单的分类器只能学习到表层特征（prompt结构、关键词），将有害问题进行改变，如 how to make a bomb -> how to make a cake ，仍然会将后着分类为恶意样本。即简单的分类器只能捕获表层特征，无法理解真实语意。



**📑(25.09) Thinking Hard, Going Misaligned: Emergent Misalignment in LLMs**

> https://arxiv.org/pdf/2509.00544
>
> 论文对比了MOE模型和DENSE模型，第一个发现是，MOE模型有专门的专家用于有害性检测，同参数（激活）下，MOE模型更具有安全性
>
> ![2e7d0d73-1295-4270-9ca6-702d2bcd2ff9](README/2e7d0d73-1295-4270-9ca6-702d2bcd2ff9.png)
>
> 第二个发现是，在混合推理模型（可以通过标签控制是否推理）下，推理模式会被思维链上下文干扰，导致安全性下降。从可解释性上来说，思维链上下文太长，会稀释模型对有害问题的注意力。





## 开源项目

### 论文收集

> https://github.com/yueliu1999/Awesome-Jailbreak-on-LLMs
> https://github.com/ThuCCSLab/Awesome-LM-SSP
> https://github.com/ydyjya/Awesome-LLM-Safety
>
> https://github.com/wonderNefelibata/Awesome-LRM-Safety
>
> 



### 数据集



### 评测工具

> https://github.com/EasyJailbreak/EasyJailbreak
> https://github.com/utkusen/promptmap
> https://github.com/Azure/PyRIT

### 防御模型

