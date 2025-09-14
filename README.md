
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



**📑(25.08) CCFC: Core & Core–Full–Core Dual-Track Defense for LLM Jailbreak Protection**

> ![image-20250912005143683](README/image-20250912005143683.png)
>
> https://arxiv.org/abs/2508.14128
>
> 对于用户输入的恶意prompt P，首先调用语言模型提取其核心意图C 。将C 和C + P + C (三明治形式)分别调用模型，根据模型响应进行二次检查。（这样会造成数倍的延迟和资源消耗，并不适合直接应用，对于加密恶意意图的有害prompt可能效果并不好）

 

**📑(25.08)The Cost of Thinking: Increased Jailbreak Risk in Large Language Models**

> https://arxiv.org/pdf/2508.10032
>
> ​	论文首先测试了qwen3 0.6B~8B 混合模型的两种模式，发现思考模型被越狱的成功率普遍增加，论文认为当让思考模型处于教育场景时更容易被越狱，即使它们思考时认为其有害。 论文给出了一个简单的有效的解决方案：在用户的query后面额外增加<Think>token，并构造一个简单的安全防护prompt，这样模型就会顺着这个安全防护prompt进行推理，从而降低了安全风险。
>
> ​	类似H-COT这种是构造思维链来绕过模型对齐，这篇是用构造思维链来加强安全对齐。







**📑(25.08) PUZZLED: Jailbreaking LLMs through Word-Based Puzzles**

> ![image-20250912004915146](README/image-20250912004915146.png)
>
> https://arxiv.org/abs/2508.01306
>
> 将带有明显恶意意图的单词转换成字谜，让模型进行复杂推理解密，从而绕过模型对齐，这种绕过思路也代表着，一些简单的对齐只能让模型在一开始输出拒绝，若增加问题复杂度，模型则会先去解密，解密出来后已经偏离了对齐。对齐若只能学到表层的模式，则存在绕过的风险。







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

**📑(24.10) FLIPATTACK: JAILBREAK LLMS VIA FLIPPING**

> https://arxiv.org/pdf/2410.02832
>
> ![7f01893e-8d69-4385-bf3e-5e136aa858af](README/7f01893e-8d69-4385-bf3e-5e136aa858af.png)
>
> ​	相比于各种编码、加密的方式去隐藏恶意意图。 Filp Attack的思路，基于简单的翻转来隐藏恶意意图。模型需要从右往左的形式来恢复恶意prompt，这种方法的优势是困惑度高，防火墙和模型本身很难在最开始识别恶意意图。翻转的级别包括句子、单词。
>
> ![image-20250913230856660](README/image-20250913230856660.png)





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





**📑(23.10)Low-Resource Languages Jailbreak GPT-4**

> ![image-20250912211446160](README/image-20250912211446160.png)
>
> https://arxiv.org/pdf/2310.02446 
>
> 论文发现小语种如 zulu语可以直接绕过模型的安全对齐，通过实验发现，使用频率越低的语言，越有可能绕过模型。这代表模型的对齐并没有较好的泛化。



**📑GPT-4 IS TOO SMART TO BE SAFE: STEALTHY CHAT WITH LLMS VIA CIPHER**

> ![77eef519-c345-402e-9bcf-9376cd816284](README/77eef519-c345-402e-9bcf-9376cd816284.png)
>
> https://arxiv.org/pdf/2308.06463
>
> 在system中指明加密交流的方式，并给一些fewshot让其理解。 随后将加密的问题发送给目标模型



> https://arxiv.org/pdf/2308.06463
>
> ![039a9ad5-96f5-47d6-8911-5d6928462cc2](README/039a9ad5-96f5-47d6-8911-5d6928462cc2.png)



## 防御 GUARD

### 2025

**📑(25.09) DynaGuard: A Dynamic Guardrail Model With User-Defined Policies**

>https://arxiv.org/pdf/2509.02563
>
>动态防御，特点是可以加规则，如在医疗场景中，需允许 “人体解剖讨论” 但禁止 “色情内容。通过合成数据集进行微调，数据集主要包含：规则、对话、推理、判断结果。
>
>![43ead334-2dd1-4d51-916b-8c8d31c9cfb5](README/43ead334-2dd1-4d51-916b-8c8d31c9cfb5.png)
>
>

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



### 数据集



### 评测工具

> https://github.com/EasyJailbreak/EasyJailbreak
>
> https://github.com/Azure/PyRIT

### 防御模型

