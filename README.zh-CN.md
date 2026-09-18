# Awesome Full-Duplex Benchmark [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

**[English](README.md) | 中文**

全双工口语对话的 **评测** 资源列表，按最终报告的骨架排：先写清楚打什么分，而不是先按 GitHub 仓库归堆。

模型与训练数据见姊妹列表：[Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM)。本仓库面向真正跑评测的人。

欢迎 PR：补充 benchmark、指标定义，或解释某个数字到底在测什么。

### 图例

**Class（能力大类）** — 这个分数在说什么。协议和赛制不是大类。每个大类有一份短说明，在 [`docs/`](docs/README.zh-CN.md)。

| Class | 小类 | 含义 |
|:--|:--|:--|
| **[Interaction](docs/interaction.zh-CN.md)** | Pause / Turn / Backchannel / Interrupt / Filter / Reject | 何时说、何时停、何时不说。 |
| **[Timing](docs/timing.zh-CN.md)** | Response latency / Stop latency / First audio / Tempo | 快慢和节奏。快不等于对。 |
| **[Content](docs/content.zh-CN.md)** | Instruction / Correction / Entity / Post-interrupt / Safety | 系统已经开过口、或被打断之后，话还对不对。 |
| **[Task](docs/task.zh-CN.md)** | Tool select / Args / Chain / Disfluency | 用户还在说话时把事办成。纯闲聊可标 N/A。 |
| **[Speech](docs/speech.zh-CN.md)** | Intelligibility / Prosody / Noise / Stability | 音频能不能用。论文覆盖薄，产品不能省。 |

**How（考法）** — 系统怎么被考。这些是列，不是章节。

| 标签 | 取值 | 含义 |
|:--|:--|:--|
| **Granularity** | System / Component | 完整对话产品 vs 检测器（EOT、打断、语义 VAD）。 |
| **Protocol** | Replay / Interactive / Offline / Event / Challenge | 回放录音；现场考官；只打已有输出；输出时间戳；冻结的共享任务。 |
| **Stimulus** | Synthetic / Real / Mixed / Text | TTS；真人（常见双通道）；两者都有；只有 STT/转写、没有波形。 |
| **Open** | Code + data / Code + weights / Code / Data / — | 实际发布了什么。`—` = 只有论文。 |

**Year** 取首次公开年份（arXiv v1、博客或仓库）。

同一篇论文可以出现在多个大类。Full-Duplex-Bench 的 v1 / v1.5 / v2 / v3 共用一个仓库，是不同协议。

---

## 覆盖图

一行是一个协议。空格表示「不是这篇的主声称」，不是「做不到」。

| Bench | 停顿 | 轮次 | 附和 | 打断 | 过滤 | 拒识 | 时延 | 节奏 | 内容 | 任务 | 语音 | 粒度 | 协议 | 中文 |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| **Full-Duplex-Bench v1** | ✓ | ✓ | ✓ | ✓ | | | ✓ | | 打断后 | | | System | Replay | ✓ |
| **Full-Duplex-Bench v1.5** | | | ✓ | ✓ | ✓ | | ✓ | | | | 韵律* | System | Replay | 部分 |
| **Full-Duplex-Bench v2** | | ✓ | | ✓ | | | | | ✓ | | | System | Interactive | |
| **Full-Duplex-Bench v3** | | ✓ | | ✓ | | | ✓ | | | ✓ | | System | Replay | |
| **FD-Bench** | | | | ✓ | 噪声 | | ✓ | | | | WER | System | Replay | |
| **MTR-DuplexBench** | | ✓ | ✓ | ✓ | | | | | ✓ | | | System | Replay + 切轮 | |
| **Game-Time** | | | | | | | | ✓ | | | | System | Interactive | |
| **SID-Bench** | | | | ✓ | 噪声 | | ✓ | | | | | Component | Event | ✓ |
| **TurnBench** | | EOT | | ✓ | | | ✓ | | | | | Component | Event | |
| **Talking Turns** | | ✓ | ✓ | ✓ | | | | | | | | Component | Offline | |
| **HumDial-FDBench** | | | | ✓ | | ✓ | ✓ | | | | | System | Challenge | ✓ |
| **Easy-Turn** | | ✓ | ✓ | ✓ | | | | | | | | Component | Event | ✓ |
| **TurnSense** | | EOU | | | | | | | | | | Component | Offline | |
| **τ-Voice** | | ✓ | ✓ | ✓ | ✓ | | ✓ | | | ✓ | | System | Interactive | |
| **Audio MultiChallenge** | | | | | | | | | ✓ | | | System | Offline | |

\* 可选 judge。只跑 v1.5 时序仍然有效。

---

## 目录

- [1. 交互控制](#1-交互控制) · [说明](docs/interaction.zh-CN.md)
- [2. 时序](#2-时序) · [说明](docs/timing.zh-CN.md)
- [3. 多轮内容](#3-多轮内容) · [说明](docs/content.zh-CN.md)
- [4. 任务与工具](#4-任务与工具) · [说明](docs/task.zh-CN.md)
- [5. 语音与稳健](#5-语音与稳健) · [说明](docs/speech.zh-CN.md)
- [相邻：语音理解与半双工 Agent](#相邻语音理解与半双工-agent)
- [商业 API 主打评测](docs/commercial.zh-CN.md) · GPT / Gemini / Grok / Seed / Qwen 官方报哪些集
- [评测数据与刺激](#评测数据与刺激)
- [指标注意事项](#指标注意事项)
- [综述](#综述)
- [相关列表](#相关列表)

---

## 1. 交互控制

何时说、何时停、何时不说。**不要**把这些小类平均成一个 TOR：停顿要少抢，接话要多接。

| 标题 | 年 | 小类 | 粒度 | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v1** | 2025 | Pause / Turn / Backchannel / Interrupt | System | Replay | Mixed | Code + data | EN / ZH | TOR（方向随任务反转）、附和频率 / JSD、takeover 时延、打断 GPT 分 | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Site](https://full-duplex-bench.github.io/) |
| **Full-Duplex-Bench v1.5** | 2025 | Interrupt / Backchannel / Filter | System | Replay | Mixed | Code + data | EN / ZH* | 行为标签、停止 / 响应时延、可选韵律 | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **FD-Bench** | 2025 | Interrupt / Filter | System | Replay | Synthetic | Code + data | EN | SIRate / SRIRate / EIRate / NIRate、IRD、FSED、WER | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench)/[Dataset](https://huggingface.co/collections/pengyizhou/fd-bench-audio-68674bd6de6feea91ba3ce37) |
| **HumDial-FDBench** | 2026 | Interrupt / Reject | System | Challenge | Real | Code + data | ZH / EN | 打断、拒识、时延；Final = 0.4 / 0.4 / 0.2 | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench)/[Dataset](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench)/[Challenge](https://aslp-lab.github.io/HumDial-Challenge/) |
| **SID-Bench** | 2026 | Interrupt / Filter | Component | Event | Real | Code + data | EN / ZH | FIR、IRL、APT | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **TurnBench** | 2026 | Turn（EOT）/ Interrupt | Component | Event | Real | Code + data | EN | EOT / INT 召回、假阳、时序；有公开榜 | [arXiv](https://arxiv.org/abs/2608.25218)/[Site](https://turnbench.sesame.com/)/[Github](https://github.com/SesameAILabs/turnbench)/[Blog](https://www.sesame.com/blog/turnbench) |
| **Talking Turns** | 2025 | Turn / Backchannel / Interrupt | Component | Offline | Real | — | EN | 轮次切换、附和、打断、抢话打断。论文承诺开源评测台，未见可用的公开 scorer | [arXiv](https://arxiv.org/abs/2503.01174)/[Apple](https://machinelearning.apple.com/research/talking-turns) |
| **Easy-Turn** | 2025 | Turn / Backchannel / Interrupt | Component | Event | Mixed | Code + data | ZH / EN | 四态检测器（complete / incomplete / backchannel / wait），自有 testset，不是系统回放 bench | [arXiv](https://arxiv.org/abs/2509.23938)/[Github](https://github.com/ASLP-lab/Easy-Turn)/[Demo](https://aslp-lab.github.io/Easy-Turn/) |
| **TurnSense**（latishab） | 2025 | Turn（EOU） | Component | Offline | Text | Code + weights | EN | 文本级 EOU，数据是 TURNS-2K。不是百融/brgroup 的 TurnSense（中英音频） | [Github](https://github.com/latishab/turnsense)/[Dataset](https://huggingface.co/datasets/latishab/turns-2k) |
| **τ-Voice** | 2026 | Turn / Interrupt / Backchannel / Filter | System | Interactive | Mixed | Code + data | EN | 响应率、打断率、选择性（忽略附和 / 旁话）。交互有分，但 pass@1 是 Task 分 | [arXiv](https://arxiv.org/abs/2603.13686)/[Github](https://github.com/sierra-research/tau2-bench)/[Blog](https://sierra.ai/blog/tau-voice-benchmarking-real-time-voice-agents-on-real-world-tasks) |

\* FDB-Zh 目前只放出 v1.5 的子集（常见的是用户附和）。不要默认中文覆盖等于英文。

v1.5 重叠场景：用户打断、用户附和、对旁人说话、背景语音。论文里常见 **responsive**（停下并回答）vs **floor-holding**（滤掉重叠、继续说）。没有绝对更好；bench 是描述性的。

TurnBench 在 **用户** 通道上打打断，对 endpoint 和级联系统成立。边听边说的原生全双工模型需要另一套打断协议。

也报告交互信号的：[FDB v3](#4-任务与工具)（接话 / 打断）、[MTR-DuplexBench](#3-多轮内容)（会话特征）、[τ-Voice](#4-任务与工具)（打断率 / 选择性）。

---

## 2. 时序

快慢和节奏。一个系统可以很快，同时很爱在停顿上误抢。

| 标题 | 年 | 小类 | 粒度 | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Game-Time** | 2025 | Tempo | System | Interactive | Synthetic | Data | EN | 时限 / 语速 / 同步说话下的指令遵循 | [arXiv](https://arxiv.org/abs/2509.26388)/[Demo](https://ga642381.github.io/Game-Time)/[Dataset](https://huggingface.co/datasets/gametime-benchmark/gametime) |
| **Full-Duplex-Bench v1** | 2025 | Response latency | System | Replay | Mixed | Code + data | EN / ZH | takeover 时延，通常只在 takeover 样本上算 | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Full-Duplex-Bench v1.5** | 2025 | Stop / response latency | System | Replay | Mixed | Code + data | EN / ZH* | 重叠下的停止 / 响应时延 | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **FD-Bench** | 2025 | Response / stop latency | System | Replay | Synthetic | Code + data | EN | IRD、FSED、ERT、EIT | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench) |
| **SID-Bench** | 2026 | Stop latency | Component | Event | Real | Code + data | EN / ZH | IRL；APT 把误打断和慢打断折在一起 | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **HumDial-FDBench** | 2026 | Response latency | System | Challenge | Real | Code + data | ZH / EN | 时延分（Final 的 0.2） | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench) |
| **Full-Duplex-Bench v3** | 2026 | Response / first audio | System | Replay | Real | Code + data | EN | 首词、调工具、任务完成时延 | [arXiv](https://arxiv.org/abs/2604.04847)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **τ-Voice** | 2026 | Response latency | System | Interactive | Mixed | Code + data | EN | Clean vs Realistic 下的语音交互时延 | [arXiv](https://arxiv.org/abs/2603.13686)/[Github](https://github.com/sierra-research/tau2-bench) |

首音 / 首包时延是产品指标。几乎没有论文把它当独立 bench；对比 API 时仍然应该报。

---

## 3. 多轮内容

系统已经开过口、被打断、或被改口之后，话还对不对。回放测不全。交互 TOR 不能代替这一类。

| 标题 | 年 | 小类 | 粒度 | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v2** | 2025 | Instruction / Correction / Entity / Safety | System | Interactive | Mixed | Code + data | EN | 轮次流畅度、指令遵循、纠错、实体追踪、安全 | [arXiv](https://arxiv.org/abs/2510.07838)/[ACL](https://aclanthology.org/2026.acl-short.4)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **MTR-DuplexBench** | 2025 | Instruction / Safety（+ 对话质量） | System | Replay + 切轮 | Mixed | — | EN | 切轮后逐轮打会话 / 质量 / 指令遵循 / 安全 | [arXiv](https://arxiv.org/abs/2511.10262) |
| **Full-Duplex-Bench v1** | 2025 | Post-interrupt | System | Replay | Mixed | Code + data | EN / ZH | 打断 GPT 分（可选 judge） | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Audio MultiChallenge** | 2025 | Instruction / Correction / Entity | System | Offline | Real | Data | EN | 量表通过率：Inference Memory、Instruction Retention、Self Coherence、Voice Editing（句中改口） | [arXiv](https://arxiv.org/abs/2512.14865)/[ACL](https://aclanthology.org/2026.acl-long.1654/)/[Dataset](https://huggingface.co/datasets/ScaleAI/audiomc)/[Leaderboard](https://scale.com/leaderboard/audiomc) |

FDB-v2 任务族：Daily（Instruction）、Correction、Entity Tracking、Safety（11 类政策）。两种节奏：Fast vs Slow。这张表上的轮次流畅度是交互，不是内容。

Audio MultiChallenge 是多轮 **上下文**，再打一条回复 — Offline，不是现场考官。Voice Editing 是 Correction；Audio-Cue 记忆是 Entity，不是交互 TOR。Self Coherence 是打分轴，不是第六小类。

MTR 的 IF / 安全题是切轮后复用的语音 QA（Llama Question、AdvBench），不是 FDB-v2 那种分阶段目标。用户改口 ≠ FDB v3 的自我修正（那是 Task Disfluency）。

小类对照、相邻语音问答集、中文缺口见 [内容说明](docs/content.zh-CN.md)。

---

## 4. 任务与工具

用户说话不流畅时把事办成。纯闲聊系统应标 **N/A**，不要打 0。

| 标题 | 年 | 小类 | 粒度 | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v3** | 2026 | Tool select / Args / Chain / Disfluency | System | Replay | 真人不流畅 | Code + data | EN | Tool F1、参数准确率、Pass@1、接话、打断 / 填充词、时延 | [arXiv](https://arxiv.org/abs/2604.04847)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Demo](https://daniellin94144.github.io/FDB-v3-demo) |
| **τ-Voice** | 2026 | Tool select / Args / Chain / Disfluency | System | Interactive | Mixed | Code + data | EN | 相对文本 τ²-bench 的 pass@1（278 道零售 / 航司 / 电信题）；Clean vs Realistic（噪声 / 口音 / 轮次） | [arXiv](https://arxiv.org/abs/2603.13686)/[Github](https://github.com/sierra-research/tau2-bench)/[Blog](https://sierra.ai/blog/tau-voice-benchmarking-real-time-voice-agents-on-real-world-tasks) |

v3 不流畅标签：填充词、停顿、犹豫、假开始、自我修正。领域：出行、金融、住房、电商。自我修正 + 多步工具链是常见失败点。

τ-Voice 复用 τ²-bench 的工具、政策和数据库核对。Task 分是 pass@1。打断率 / 选择性归 Interaction；时延归 Timing。纯文本 τ-bench / BFCL 不进这个列表。

Gemini 博客还报过闭源的 **ComplexFuncBench Audio** 函数调用集。公开的 [ComplexFuncBench](https://github.com/zai-org/ComplexFuncBench) 是文本；音频版在这里不是可复跑协议。

---

## 5. 语音与稳健

音频能不能用。这一类在文献里很薄，最终报告里仍应占一格。

| 标题 | 年 | 小类 | 粒度 | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **FD-Bench** | 2025 | Intelligibility / Noise | System | Replay | Synthetic | Code + data | EN | WER；噪声间隙上的 NIRate | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench) |
| **Full-Duplex-Bench v1.5** | 2025 | Prosody | System | Replay | Mixed | Code + data | EN / ZH* | 重叠下可选的韵律适应 | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **SID-Bench** | 2026 | Noise | Component | Event | Real | Code + data | EN / ZH | 噪声 / 静音上的 APT 与 FIR | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |

仍缺独立公开 bench 的：回声 / 串音、无响应率、中途掉线、以及针对模型语音的可懂度集。产品评测即使论文列表填不满，也该自己补。

---

## 相邻：语音理解与半双工 Agent

这些打的是 **语音进、内容或工具**，不是全双工地板控制。GPT Realtime / Gemini Live 的数字经常出现在这里。不要和交互 TOR 混比。各家*自己主打*哪些集，见 [商业 API 主打评测](docs/commercial.zh-CN.md)。

| 标题 | 年 | 打什么分 | 为什么是相邻 | Open | 语言 | 资源 |
|:--|:-:|:--|:--|:-:|:-:|:--|
| **VoiceBench** | 2024 | 知识、指令遵循、安全；口音 / 混响 | 语音问答，没有重叠协议 | Code + data | EN | [arXiv](https://arxiv.org/abs/2410.17196)/[Github](https://github.com/MatthewCYM/VoiceBench) |
| **WildSpeech-Bench** | 2025 | 单轮 S2S 内容、副语言、噪声 | 真人问句，仍是一问一答，不是双工 | Code + data | EN | [arXiv](https://arxiv.org/abs/2506.21875)/[Github](https://github.com/Tencent/WildSpeech-Bench)/[Dataset](https://huggingface.co/datasets/tencent/WildSpeech-Bench) |
| **VocalBench** | 2025 | 回复质量、声学、会话流畅 | 半双工语音对话；有中文子集 | Code + data | EN / ZH | [arXiv](https://arxiv.org/abs/2505.15727)/[Github](https://github.com/SJTU-OmniAgent/VocalBench)/[中文](https://github.com/SJTU-OmniAgent/VocalBench-zh) |
| **VoiceAgentBench** | 2025 | 选工具 / 填参 / 多步 / 安全 | 会调工具，不打抢话 | Code + data | EN + 印度语 | [arXiv](https://arxiv.org/abs/2510.07978)/[Github](https://github.com/ola-krutrim/VoiceAgentBench)/[Dataset](https://huggingface.co/datasets/krutrim-ai-labs/VoiceAgentBench) |
| **AudioCRAG** | 2025 | 带网页 / 知识图谱工具的语音事实问答 | 语音 RAG（出自 Stream RAG），不考地板 | Data | EN | [arXiv](https://arxiv.org/abs/2510.02044) |
| **URO-Bench** | 2025 | S2S 理解 / 推理 / 口语，含多轮 | 轮转口语对话；有中文 | Code + data | EN / ZH | [arXiv](https://arxiv.org/abs/2502.17810)/[Github](https://github.com/Ruiqi-Yan/URO-Bench)/[Dataset](https://huggingface.co/datasets/Honggao/URO-Bench) |
| **VoiceAssistant-Eval** | 2025 | 听 / 说 / 看；多轮 IF 与安全 | Omni 助手，不考叠说 | Code + data | EN | [arXiv](https://arxiv.org/abs/2509.22651)/[Github](https://github.com/mathllm/VoiceAssistant-Eval) |
| **SpeechInstructBench** | 2025 | 中英指令遵循（封闭 / 开放 / 调整） | 半双工 IF，口音 / 噪声 / 不流畅 | Code + data | ZH / EN | [arXiv](https://arxiv.org/abs/2503.02769)/[Github](https://github.com/dingdongwang/SpeechInstructBench) |
| **Speech-IFEval** | 2025 | 语音模型上的文本输出约束 | 把 IF 遗忘和 ASR 拆开；不是地板 | Code | EN | [arXiv](https://arxiv.org/abs/2505.19037)/[Github](https://github.com/kehanlu/Speech-IFEval) |
| **TELEVAL** | 2025 | 中文内容兑现 + 交互得体 | 用户向中文 SLM，不是 FDB 考官 | Code + data | ZH | [arXiv](https://arxiv.org/abs/2507.18061)/[Github](https://github.com/Tele-AI/TELEVAL)/[Dataset](https://huggingface.co/datasets/Tele-AI/TELEVAL) |
| **Big Bench Audio** | 2024 | 音频推理（BBH TTS：谬误 / 导航 / 计数 / Web of Lies） | 厂商 + AA 主打；不是地板 | Data | EN | [Hugging Face](https://huggingface.co/datasets/ArtificialAnalysis/big_bench_audio)/[AA S2S](https://artificialanalysis.ai/speech-to-speech) |
| **AA Speech-to-Speech 指数** | 2026 | BBA + FDB 子集 + τ-Voice 等权；另报 TTFA | 合成记分牌，不是新协议。三腿要拆开看 | — | EN | [榜](https://artificialanalysis.ai/speech-to-speech)/[说明](https://artificialanalysis.ai/articles/announcing-the-artificial-analysis-speech-to-speech-index)/[HF 组织](https://huggingface.co/datasets/ArtificialAnalysis) |

---

## 评测数据与刺激

这里不是训练集。这些是 bench 真正回放或标注的音频来源。

| 标题 | 年 | 被谁用 | Open | 说明 | 资源 |
|:--|:-:|:--|:-:|:--|:-:|
| **CANDOR** | 2023 | FDB v1 停顿 / 轮次 | Data | 真人英语视频对话（Science Advances，不是 PNAS）；FDB 切出停顿与平滑轮次 | [Paper](https://www.science.org/doi/10.1126/sciadv.adf3197) |
| **ICC**（In Conversation Corpus） | 2024 | FDB v1 附和 | Data | 55 段上的多听者附和时序。完整 ICC 受 IRB 限制；FDB 用的是放出的附和响应 | [Umair et al.](https://arxiv.org/abs/2410.16044)/[ACL](https://aclanthology.org/2024.findings-emnlp.909/) |
| **FDB synthetic sets** | 2025 | FDB v1 打断 / 停顿 | Code + data | 带受控停顿和抢话的 TTS 用户音频 | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Full-Duplex-Bench-zh** | 2025 | FDB v1 / 部分 v1.5 | Data | 中文回放集；子集覆盖 ≠ 英文 | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **TURNS-2K** | 2025 | TurnSense（latishab） | Data | 2k 条英文 **文本** 轮次 + 二值 EOU，不是波形 | [Hugging Face](https://huggingface.co/datasets/latishab/turns-2k) |
| **Easy Turn testset** | 2025 | Easy-Turn | Data | 800 条：complete/incomplete 各 300，backchannel/wait 各 100；真人 + TTS，人工标状态 | [Github](https://github.com/ASLP-lab/Easy-Turn) |
| **HumDial-FDBench audio** | 2026 | HumDial | Data | 带重叠的双通道真人对话 | [Hugging Face](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench) |
| **TurnBench conversations** | 2026 | TurnBench | Data | 约 30 小时棚内双通道，6 类对话，三人标注 EOT / INT | [Viewer](https://turnbench.sesame.com/conversations) |
| **Game-Time tasks** | 2025 | Game-Time | Data | 时序 / 语速 / 同步类游戏任务 | [Hugging Face](https://huggingface.co/datasets/gametime-benchmark/gametime) |
| **Audio MultiChallenge** | 2025 | Audio MultiChallenge | Data | 452 段真人多轮对话，47 名说话人，1,712 条量表 | [Hugging Face](https://huggingface.co/datasets/ScaleAI/audiomc) |
| **τ²-bench 任务** | 2025 | τ-Voice | Code + data | 278 道零售 / 航司 / 电信工具题；语音层是模拟器，不是静态波形集 | [Github](https://github.com/sierra-research/tau2-bench) |
| **Big Bench Audio** | 2024 | AA S2S / 厂商博客 | Data | 1,000 条英文 TTS，23 个 Speech Arena 音色；不是双工流 | [Hugging Face](https://huggingface.co/datasets/ArtificialAnalysis/big_bench_audio) |
| **VoxPopuli-Cleaned-AA** | 2026 | AA-WER 转写 | Data | 清洗过的议会转写；AA-WER 的 25% | [Hugging Face](https://huggingface.co/datasets/ArtificialAnalysis/VoxPopuli-Cleaned-AA) |
| **Earnings22-Cleaned-AA** | 2026 | AA-WER 转写 | Data | 清洗过的财报电话转写；AA-WER 的 25% | [Hugging Face](https://huggingface.co/datasets/ArtificialAnalysis/Earnings22-Cleaned-AA) |

训练规模的双工语料（DuplexChat、DuplexGen、SmoothConv、SOMMELIER 等）放在 [模型向列表](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM#datasets)。

---

## 指标注意事项

忽略这些细节，两篇论文的数字就不能直接比。

1. **TOR 不是同一个数。** FDB v1 里，停顿处理的 takeover rate 是 **越低越好**，平滑轮次交接和用户打断是 **越高越好**。写 TOR 时一定带上小类。不要把 Interaction 平均成一个总分。
2. **FDB 附和规则。** 官方代码把「时长 < 1 秒 **且** 词数 ≤ 3」算作 backchannel。不满足这条的短促漏音仍算 takeover。如果你关心「停顿期间模型有没有出声」，另加更严的能量型比率。
3. **时延分母不一样。** 有的 bench 对全部样本平均时延；FDB 轮次时延通常只在 takeover 样本上算。SID-Bench 的 APT 把误打断和慢打断折进同一个惩罚。时序是第 2 类，不能代替第 1 类。
4. **产品 VAD 是系统的一部分。** 把每家 API 的 `silence_duration_ms` 调成一样并不更「公平」，那是另一个产品。分数旁边写出发货默认值（或你实际拧过的旋钮）。
5. **回放 ≠ 对话。** Replay 测不了「模型自己的声音会不会触发下一轮用户事件」。第 3 类需要 Interactive（FDB-v2）、切轮器（MTR）或真人。成本更高，也会随考官模型漂移。
6. **合成重叠很干净。** TTS 抢话起音利落、串音少。真人双通道（TurnBench、HumDial、SID-Bench）有附和、回声、句中停顿，会抬高打断假阳。
7. **Judge 指标可选且贵。** FDB v1 打断 GPT 分、v1.5 行为 / 韵律 judge 需要额外模型凭证。只跑时序仍然有效；不要把有 judge 和没 judge 的榜混在一起。
8. **中文覆盖不均匀。** 不少论文写 multilingual，只是因为有一个中文子集。声称中文结果前，先核对哪些任务真的翻译了。
9. **组件 ≠ 系统。** EOT 检测器分数不是对话产品分数。粒度要写在明处。Challenge 分数只在该冻结协议下可比。
10. **相邻 ≠ 交互。** VoiceBench / WildSpeech / VocalBench / Big Bench Audio 是语音理解或音频推理。那边分高，不代表能把地板握住。τ-Voice 的 pass@1 是 Task；打断率才是 Interaction。
11. **AA S2S 是三个大类的平均。** Artificial Analysis 等权折 Big Bench Audio、FDB 子集和 τ-Voice。要报腿，不要只报合成分。他们 HF 组织里还有转写清洗和文本 Intelligence 集 — 那些不是全双工对话。

---

## 综述

| 标题 | 年 | 对评测有什么用 | 资源 |
|:--|:-:|:--|:-:|
| **A Survey of Full-Duplex Spoken Dialogue Systems: Architectural Hierarchy, Interaction Ontology, and Decision State Machine** | 2026 | 交互本体与决策状态 — 给指标命名时有用 | [arXiv](https://arxiv.org/abs/2606.19453)/[Github](https://github.com/DuplexLM/DuplexSurvey) |
| **From Turn-Taking to Synchronous Dialogue: A Survey of Full-Duplex Spoken Language Models** | 2025 | 梳理半双工 vs 全双工的评测缺口 | [arXiv](https://arxiv.org/abs/2509.14515)/[Github](https://github.com/elpsykongloo/FD-SLMs) |

---

## 相关列表

- [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM) — 模型、组件、训练数据。
- [Full-Duplex-Bench](https://github.com/DanielLin94144/Full-Duplex-Bench) — 目前最完整的开源评测套件（v1 / v1.5 / v2 / v3）。
- [Artificial Analysis Speech-to-Speech](https://artificialanalysis.ai/speech-to-speech) — 独立榜：重跑 Big Bench Audio + FDB 子集 + τ-Voice。

---

## 贡献

见 [CONTRIBUTING.md](CONTRIBUTING.md)（[中文](CONTRIBUTING.zh-CN.md)）。条目放进**实际被打分的那个大类**，不要按会议或仓库归堆。同一篇论文可以出现在多个大类。改表时必须同时改 **`README.md` 和 `README.zh-CN.md`**。
