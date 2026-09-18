# 商业 API 主打评测

**[目录](../README.zh-CN.md) · [English](commercial.md)**

厂商发版博客上的数字，**不是**一张全双工成绩单。官方数字多半是语音理解、音频推理或工具调用。地板控制要么是内部指标，要么要等第三方 bench 去打他们的 API。

这一页只记 **他们主打哪些集**，不是排行榜。分数会随模型版本变。

## 官方 vs 第三方

| 种类 | 谁跑 | 常见集 | 能声称什么 |
|:--|:--|:--|:--|
| **官方主打** | 厂商自己 | Big Bench Audio、VoiceBench、ComplexFuncBench Audio、内部 MOS | 协议是他们定的。常常不是交互 TOR |
| **第三方差全双工** | FDB / τ-Voice / [Artificial Analysis](https://artificialanalysis.ai/speech-to-speech) | FDB（AA 用子集）、τ-Voice | 地板 + 工具可横向比（前提是真的打了这个 API） |
| **第三方相邻** | Scale、VoiceBench 作者、Coval、AA | Audio MultiChallenge、VoiceBench、WildSpeech、Big Bench Audio | 内容 / 推理 / 时延。不要和 [交互](interaction.zh-CN.md) 混 |

好几个其实不是「数据集」。FDB v2、τ-Voice、OpenAI 的 RUN、Seed 的真人测，都是 **协议**（模拟器、考官或现场通话），不是一包冻住的 wav。

## 各家主打什么

### GPT Realtime（OpenAI）

| 他们报 | 对应大类 | 说明 | 来源 |
|:--|:--|:--|:--|
| **Big Bench Audio** | 相邻（音频推理） | 发版博主打。不是停顿 / 打断 | [gpt-realtime](https://openai.com/index/introducing-gpt-realtime/) |
| 内部字母数字串（电话 / VIN，多语） | 内容 / 语音 | 没有公开划分 | 同上 |
| Cookbook **CRAWL / WALK / RUN** | 时序 / 交互 / 任务 | 他们推荐的产品评测。RUN 是全双工模拟主叫；文档写明借鉴了 τ-Voice。不是放出的共享集 | [Realtime eval guide](https://developers.openai.com/cookbook/examples/audio/voice_agent_evaluation) |

第三方还会拿 Realtime 跑 [FDB v2](../README.zh-CN.md#3-多轮内容)、[FDB v3](../README.zh-CN.md#4-任务与工具)、[τ-Voice](../README.zh-CN.md#4-任务与工具)、[Audio MultiChallenge](../README.zh-CN.md#3-多轮内容)，以及 [AA Speech-to-Speech 指数](#artificial-analysis-speech-to-speech-指数)。

### Gemini Live / Native Audio（Google）

| 他们报 | 对应大类 | 说明 | 来源 |
|:--|:--|:--|:--|
| **ComplexFuncBench Audio** | 任务（闭源） | 2025-12 原生音频博文 71.5%。公开的 [ComplexFuncBench](https://github.com/zai-org/ComplexFuncBench) 是文本；音频版在这里不可复跑 | [Gemini 音频更新](https://blog.google/products-and-platforms/products/gemini/gemini-audio-model-updates/) |
| 内部指令遵循 | 内容 | 同文 90%；题目不公开 | 同上 |
| 未命名的多轮上下文 | 内容 | 只有博客说法 | 同上 |

第三方还会拿 Live / Gemini 音频跑 FDB v3、τ-Voice、Audio MultiChallenge、VoiceBench。论文里 Audio MultiChallenge 最高是 Gemini 3 Pro Thinking（54.65% pass）。

### Grok Voice（xAI）

| 他们报 | 对应大类 | 说明 | 来源 |
|:--|:--|:--|:--|
| **Big Bench Audio** | 相邻（音频推理） | 发版自称；AA 也把它当作 S2S 指数的推理腿 | [Grok Voice Agent API](https://x.ai/news/grok-voice-agent-api) |
| 首音时延 | 时序 | 产品宣称亚秒 | 同上 |
| 对人盲测 vs OpenAI Realtime | 语音 | 发音 / 口音 / 韵律，不是 TOR | 同上 |

第三方还会拿 Grok Voice 跑 FDB v3、τ-Voice 和 AA 的 S2S 指数。Audio MultiChallenge 论文表里没有它。

### Seeduplex / SeedDuplex（字节 Seed）

| 他们报 | 对应大类 | 说明 | 来源 |
|:--|:--|:--|:--|
| 判停 MOS、对话流畅 MOS | 交互 / 时序 | 相对豆包上一版半双工 +8% / +12% | [Seeduplex](https://research.doubao.com/zh/seeduplex) |
| 抢话率、打断响应时延、误回 / 误打断 | 交互 / 时序 | 相对自家半双工的差值；复杂声学场景 | 同上 |
| 真人人人对话基线 | 交互 | 产品 MOS，没有公开 scorer | 同上 |
| 「主流 App 语音通话」横评 | — | 对手未点名 | 同上 |

厂商没有公开的 FDB / τ-Voice / VoiceBench 行。这些按 **内部产品指标** 看。

### Qwen-Omni（阿里）

| 他们报 | 对应大类 | 说明 | 来源 |
|:--|:--|:--|:--|
| **VoiceBench** | 相邻 | 官方语音对话主打（技术报告里 Qwen3-Omni-Thinking 89.5） | [Qwen3-Omni](https://github.com/QwenLM/Qwen3-Omni) / [arXiv 2509.17765](https://arxiv.org/abs/2509.17765) |
| MMAU / MMSU | 相邻（音频推理） | 不是对话地板 | 同上 |
| ASR / S2TT / 音乐集 | — | 理解，不是双工 | 同上 |
| 首包时延（234 ms） | 时序 | 系统测量，不是 FDB | 同上 |

技术报告 **没有** 把 FDB 或 τ-Voice 当主打。Audio MultiChallenge 里有 Qwen3-Omni（音频输出，24.34% pass）。AA 的 S2S 榜现在也列了 Qwen realtime 在 Big Bench Audio / FDB / τ-Voice 上的分。

## Artificial Analysis Speech-to-Speech 指数

这是主要的 **独立商业记分牌**，不是新协议。[公告](https://artificialanalysis.ai/articles/announcing-the-artificial-analysis-speech-to-speech-index) / [实时榜](https://artificialanalysis.ai/speech-to-speech)。他们托管或清洗的数据在 [huggingface.co/datasets/ArtificialAnalysis](https://huggingface.co/datasets/ArtificialAnalysis)。

三腿等权（旁边另报 TTFA / 价格）：

| AA 腿 | 对应这里 | 公开产物 | 不是 |
|:--|:--|:--|:--|
| **Speech Reasoning** | 相邻（音频推理） | [Big Bench Audio](https://huggingface.co/datasets/ArtificialAnalysis/big_bench_audio) — 1,000 条英文 TTS，来自 BBH（Formal Fallacies、Navigate、Object Counting、Web of Lies） | 你已经开过口之后的指令 |
| **Conversational Dynamics** | 交互 | Full-Duplex-Bench **子集**（停顿 / 轮次 / 打断 / 附和） | 他们的合成分 ≠ FDB 论文原表 |
| **Agentic Performance** | 任务 | τ-Voice（航司 / 零售 / 电信） | Cookbook RUN |

**不要**把 AA 的一个百分数当成交互 TOR。它平均了三个大类。

同一 HF 组织里、**不是** S2S 对话的：

| HF 仓库 | AA 产品 | 对应大类 |
|:--|:--|:--|
| `VoxPopuli-Cleaned-AA`、`Earnings22-Cleaned-AA` | [AA-WER](https://artificialanalysis.ai/articles/aa-wer-v2) 转写（另有未公开的 **AA-AgentTalk**） | [语音](speech.zh-CN.md) 转写，不是双工模型语音 |
| `AA-LCR`、`AA-Omniscience-Public`、`AA-Briefcase-Lite`、`ITBench-AA` | 文本 Intelligence Index | 不进这个列表 |

## 第三方覆盖（谁真的被打过）

空格 = 那篇论文的表里没有，不是「这个 API 跑不了」。

| Bench | GPT Realtime | Gemini Live | Grok Voice | Seeduplex | Qwen-Omni |
|:--|:--:|:--:|:--:|:--:|:--:|
| **FDB v2** | ✓ | | | | |
| **FDB v3** | ✓ | ✓ | ✓ | | |
| **τ-Voice** | ✓ | ✓ | ✓ | | |
| **Audio MultiChallenge** | ✓ | ✓ | | | ✓ |
| **VoiceBench** | GPT-4o-Audio* | ✓ | | | ✓（官方） |
| **Coval S2S** | ✓ | ✓ | | | |
| **AA S2S 指数** | ✓ | ✓ | ✓ | | ✓* |

\* VoiceBench 表里常见的是 GPT-4o-Audio，不一定是后来的 Realtime SKU。AA 后来的 S2S 榜列了 Qwen realtime；Seeduplex 仍没出现。

如果只要一套能同时打到 GPT、Gemini、Grok **地板 + 工具** 的公开栈：FDB v3 和 τ-Voice — 或者看 AA 指数但必须 **拆开三腿**。多轮内容再加 Audio MultiChallenge。Seed 的空缺，不要用 VoiceBench 或 MOS 去填 Interaction。

## 不要混比

1. Big Bench Audio / VoiceBench / MMAU / AA 合成分 ≠ [交互](interaction.zh-CN.md) 的 TOR。
2. ComplexFuncBench Audio ≠ FDB v3 / τ-Voice。同属任务大类，协议不同，而且音频集闭源。
3. Seed 的 MOS 差值是对豆包半双工，不是对 GPT。
4. OpenAI RUN 和 τ-Voice 是近亲，不是同一套 harness。Cookbook 分数不是 τ-Voice 的 pass@1。
5. 博客写「行业领先」却不给可复跑协议的，不要写进覆盖图。

半双工条目见 [相邻](../README.zh-CN.md#相邻语音理解与半双工-agent)。一个数字允许代表什么，见五个大类说明。
