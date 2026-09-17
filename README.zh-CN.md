# Awesome Full-Duplex Benchmark [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

**[English](README.md) | 中文**

全双工口语对话的 **评测** 资源列表：benchmark、指标、协议、挑战赛、以及组件级测试。

模型与训练数据见姊妹列表：[Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM)。本仓库面向真正跑评测的人。

欢迎 PR：补充 benchmark、指标定义，或解释某个数字到底在测什么。

### 图例

**Focus（评测焦点）** — 这条条目实际在测什么：

| Focus | 含义 |
|:--|:--|
| **Interaction** | 停顿、轮次交接、附和（backchannel）、打断、重叠。 |
| **Multi-turn** | 多轮一致性、纠错、实体追踪、安全。 |
| **Tool-use** | 在实时语音 / 不流畅条件下调用工具。 |
| **Temporal** | 何时开口、语速、有意同步叠说。 |
| **Component** | 检测器，不是完整对话系统：EOT、打断、语义 VAD。 |
| **Challenge** | 协议冻结的共享任务 / 排行榜。 |

**Protocol（协议）** — 系统怎么被考：

| Protocol | 含义 |
|:--|:--|
| **Replay** | 回放录好的用户音频，录模型音频，离线打分。 |
| **Interactive** | 现场考官或双智能体闭环（WebRTC / WebSocket）。 |
| **Offline** | 只给已有音频或模型输出打分，不连实时 API。 |
| **Event** | 模型在双通道语音上输出时间戳 / 标签。 |

**Stimulus（刺激）** — 用户音频从哪来：

| Stimulus | 含义 |
|:--|:--|
| **Synthetic** | LLM 文本 + TTS。好扩规模，缺真人时序和韵律。 |
| **Real** | 真人录音，常见双通道。 |
| **Mixed** | 两者都有，或在真人语音上插入合成重叠。 |

**Open（开放程度）** — 实际发布了什么：

| Open | 含义 |
|:--|:--|
| **Code + data** | 评测能跑，音频 / 标签也公开。 |
| **Code** | 有公开仓库；数据缺失、gated，或没挂链接。 |
| **Data** | 音频 / 标签公开；打分代码很薄或没有。 |
| **—** | 只有论文或技术报告。 |

**Year** 取首次公开年份（arXiv v1、博客或仓库）。

---

## 覆盖图

用这张表选 bench。一行是一个协议，不是一个 GitHub 仓库。Full-Duplex-Bench 的 v1 / v1.5 / v2 / v3 共用一个仓库，测的不是同一件事。

| Bench | 停顿 | 轮次 | 附和 | 打断 | 重叠过滤 | 多轮 | 工具 | 时序 | 刺激 | 中文 | 协议 |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--|
| **Full-Duplex-Bench v1** | ✓ | ✓ | ✓ | ✓ | | | | | Mixed | ✓ | Replay |
| **Full-Duplex-Bench v1.5** | | | ✓ | ✓ | ✓ | | | | Mixed | 部分 | Replay |
| **Full-Duplex-Bench v2** | | ✓ | | ✓ | | ✓ | | | Interactive | | Interactive |
| **Full-Duplex-Bench v3** | | ✓ | | ✓ | | ✓ | ✓ | | Real | | Replay / agent |
| **FD-Bench** | | | | ✓ | 噪声 | | | | Synthetic | | Replay |
| **MTR-DuplexBench** | | ✓ | ✓ | ✓ | | ✓ | | | Mixed | | Replay + 切轮 |
| **Game-Time** | | | | | | | | ✓ | Synthetic | | Interactive / 任务 |
| **SID-Bench** | | | | ✓ | 噪声 | | | | Real | ✓ | Event |
| **TurnBench** | | EOT | | ✓ | | | | | Real | | Event |
| **Talking Turns** | | ✓ | ✓ | ✓ | | | | | Real | | Offline / 预测 |
| **HumDial-FDBench** | | | | ✓ | 拒识 | | | | Real | ✓ | Challenge |

空格表示「不是这篇的主声称」，不是「做不到」。

---

## 目录

- [系统级交互](#系统级交互)
- [重叠与打断](#重叠与打断)
- [交互式多轮](#交互式多轮)
- [工具调用与 Agent](#工具调用与-agent)
- [时序动态](#时序动态)
- [组件级测试](#组件级测试)
- [挑战赛与榜单](#挑战赛与榜单)
- [评测数据与刺激](#评测数据与刺激)
- [指标注意事项](#指标注意事项)
- [综述](#综述)
- [相关列表](#相关列表)

---

## 系统级交互

把用户波形回放到在线系统里，再打 takeover、时延，有时还有回复质量。这是比较商业实时 API 和开源级联栈最便宜的办法。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench** | 2025 | Interaction | Replay | Mixed | Code + data | EN / ZH | TOR、附和频率 / JSD、takeover 时延、打断 GPT 分 | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Site](https://full-duplex-bench.github.io/) |
| **FD-Bench** | 2025 | Interaction | Replay | Synthetic | Code + data | EN | SIRate / SRIRate / EIRate / NIRate、IRD、FSED、WER | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench)/[Dataset](https://huggingface.co/collections/pengyizhou/fd-bench-audio-68674bd6de6feea91ba3ce37) |
| **MTR-DuplexBench** | 2025 | Multi-turn + interaction | Replay + 切轮 | Mixed | — | EN | 会话特征、对话质量、指令遵循、安全 | [arXiv](https://arxiv.org/abs/2511.10262) |

v1 任务：停顿处理、附和、平滑轮次交接、用户打断。TOR **方向随任务反转** — 见 [指标注意事项](#指标注意事项)。

---

## 重叠与打断

语音叠在语音上，才是全双工真正难的地方。这些 bench 问的是：模型该停、该继续、该附和，还是把重叠当噪声。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v1.5** | 2025 | Overlap | Replay | Mixed | Code + data | EN / ZH* | 行为标签、停止 / 响应时延、可选韵律 | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Semantic-Aware Interruption Detection (SID-Bench)** | 2026 | Component — 打断 | Event | Real | Code + data | EN / ZH | FIR、IRL、APT | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **HumDial-FDBench** | 2026 | Challenge — 打断 / 拒识 | Challenge | Real | Code + data | ZH / EN | 打断、拒识、时延分 | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench)/[Dataset](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench)/[Challenge](https://aslp-lab.github.io/HumDial-Challenge/) |

\* FDB-Zh 目前只放出 v1.5 的子集（常见的是用户附和）。不要默认中文覆盖等于英文。

v1.5 重叠场景：用户打断、用户附和、对旁人说话、背景语音。论文里常见两种策略 — **responsive**（停下并快速回答）vs **floor-holding**（滤掉重叠、继续说）。没有绝对更好；bench 是描述性的。

---

## 交互式多轮

回放测不了「系统自己说过话之后还能不能保持连贯」。这类设置把考官（或切轮器）放进闭环。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v2** | 2025 | Multi-turn | Interactive | Examiner | Code + data | EN | 轮次流畅度、指令遵循、纠错、实体追踪、安全 | [arXiv](https://arxiv.org/abs/2510.07838)/[ACL](https://aclanthology.org/2026.acl-short.4)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **MTR-DuplexBench** | 2025 | Multi-turn | Replay + 切轮 | Mixed | — | EN | 切轮后逐轮打会话 / 质量 / 指令遵循 / 安全 | [arXiv](https://arxiv.org/abs/2511.10262) |

FDB-v2 任务族：Daily、Correction、Entity Tracking、Safety。两种节奏：Fast vs Slow。

---

## 工具调用与 Agent

全双工质量不只是轮次交接。Agent 还要在用户说话不流畅时把工具调对。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v3** | 2026 | Tool-use | Replay / agent | 真人不流畅 | Code + data | EN | Tool F1、参数准确率、Pass@1、接话、打断 / 填充词、时延 | [arXiv](https://arxiv.org/abs/2604.04847)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Demo](https://daniellin94144.github.io/FDB-v3-demo) |

v3 不流畅标签：填充词、停顿、犹豫、假开始、自我修正。领域：出行、金融、住房、电商。自我修正 + 多步工具链是常见失败点。

---

## 时序动态

多数 bench 打的是用户停下来之后 *发生了什么*。这些打的是模型 *何时* 开口，包括故意叠说。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Game-Time** | 2025 | Temporal | Interactive / 任务 | Synthetic | Data | EN | 时限 / 语速 / 同步说话下的指令遵循 | [arXiv](https://arxiv.org/abs/2509.26388)/[Demo](https://ga642381.github.io/Game-Time)/[Dataset](https://huggingface.co/datasets/gametime-benchmark/gametime) |

---

## 组件级测试

只打轮次检测、endpoint、打断头，不必拉起完整对话产品。适合在级联栈里换 VAD / 语义轮次模块时用。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **TurnBench** | 2026 | Component — EOT + 打断 | Event | 真人双通道 | Code + data | EN | EOT / INT 召回、假阳、时序 | [arXiv](https://arxiv.org/abs/2608.25218)/[Site](https://turnbench.sesame.com/)/[Github](https://github.com/SesameAILabs/turnbench)/[Blog](https://www.sesame.com/blog/turnbench) |
| **Talking Turns** | 2025 | Component — 事件预测 | Offline | Real | — | EN | 轮次切换、附和、打断、抢话打断 | [arXiv](https://arxiv.org/abs/2503.01174) |
| **SID-Bench** | 2026 | Component — 语义打断 | Event | Real | Code + data | EN / ZH | FIR、IRL、APT | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **Easy-Turn** | 2025 | Component — 轮次检测 | Event | Mixed | Code | ZH / EN | 轮次检测（模型论文带评测） | [arXiv](https://arxiv.org/abs/2509.23938)/[Github](https://github.com/ASLP-lab/Easy-Turn)/[Demo](https://aslp-lab.github.io/Easy-Turn/) |
| **TurnSense** | 2025 | Component — EOU | Event | Real | Code + weights | EN / ZH | 句末检测 | [Github](https://github.com/latishab/turnsense)/[Dataset](https://huggingface.co/datasets/latishab/turns-2k) |

TurnBench 说明：在 **用户** 通道上打打断，对 endpoint 和级联系统成立。边听边说的原生全双工模型需要另一套打断协议；作者原文写了这一点。

---

## 挑战赛与榜单

协议冻结、公开排名，常有 hidden test。适合要一个可比较的总分；不适合你想改指标的时候。

| 标题 | 年 | Focus | Protocol | Stimulus | Open | 语言 | 核心指标 | 资源 |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **HumDial-FDBench**（ICASSP 2026 HumDial） | 2026 | Challenge | Challenge | 真人双通道 | Code + data | ZH / EN | Final = 0.4 打断 + 0.4 拒识 + 0.2 时延 | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench)/[Challenge](https://aslp-lab.github.io/HumDial-Challenge/) |
| **TurnBench leaderboard** | 2026 | Component | Event | Real | Code + data | EN | 冻结工作点上的 EOT / INT 召回 vs 假阳 | [Site](https://turnbench.sesame.com/) |

---

## 评测数据与刺激

这里不是训练集。这些是 bench 真正回放或标注的音频来源。

| 标题 | 年 | 被谁用 | Open | 说明 | 资源 |
|:--|:-:|:--|:-:|:--|:-:|
| **CANDOR** | 2023 | FDB v1 停顿 / 轮次交接 | Data | 真人双方对话；FDB 切出停顿与平滑轮次 | [Paper](https://www.pnas.org/doi/10.1073/pnas.2218522120) |
| **ICC**（In Conversation Corpus） | 2024 | FDB v1 附和 | Data | 多听者附和时序；FDB 用 TOR / 频率 / JSD 对齐该分布 | [Umair et al.](https://arxiv.org/abs/2402.02889) |
| **FDB synthetic sets** | 2025 | FDB v1 打断 / 停顿 | Code + data | 带受控停顿和抢话的 TTS 用户音频 | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Full-Duplex-Bench-zh** | 2025 | FDB v1 / 部分 v1.5 | Data | 中文回放集；子集覆盖 ≠ 英文 | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **TURNS-2K** | 2025 | TurnSense | Data | EOU 标签 | [Hugging Face](https://huggingface.co/datasets/latishab/turns-2k) |
| **HumDial-FDBench audio** | 2026 | HumDial 挑战赛 | Data | 带重叠的双通道真人对话 | [Hugging Face](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench) |
| **TurnBench conversations** | 2026 | TurnBench | Data | 约 30 小时棚内双通道，6 类对话，三人标注 EOT / INT | [Viewer](https://turnbench.sesame.com/conversations) |
| **Game-Time tasks** | 2025 | Game-Time | Data | 时序 / 语速 / 同步类游戏任务 | [Hugging Face](https://huggingface.co/datasets/gametime-benchmark/gametime) |

训练规模的双工语料（DuplexChat、DuplexGen、SmoothConv、SOMMELIER 等）放在 [模型向列表](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM#datasets)。

---

## 指标注意事项

忽略这些细节，两篇论文的数字就不能直接比。

1. **TOR 不是同一个数。** FDB v1 里，停顿处理的 takeover rate 是 **越低越好**，平滑轮次交接和用户打断是 **越高越好**。写 TOR 时一定带上任务名。
2. **FDB 附和规则。** 官方代码把「时长 < 1 秒 **且** 词数 ≤ 3」算作 backchannel。不满足这条的短促漏音仍算 takeover。如果你关心「停顿期间模型有没有出声」，另加更严的能量型比率。
3. **时延分母不一样。** 有的 bench 对全部样本平均时延；FDB 轮次时延通常只在 takeover 样本上算。SID-Bench 的 APT 把误打断和慢打断折进同一个惩罚。
4. **产品 VAD 是系统的一部分。** 把每家 API 的 `silence_duration_ms` 调成一样并不更「公平」，那是另一个产品。分数旁边写出发货默认值（或你实际拧过的旋钮）。
5. **回放 ≠ 对话。** Replay bench 测不了「模型自己的声音会不会触发下一轮用户事件」。FDB-v2 / Game-Time / 真人挑战赛把这个闭环补上；成本更高，也会随考官模型漂移。
6. **合成重叠很干净。** TTS 抢话起音利落、串音少。真人双通道（TurnBench、HumDial、SID-Bench）有附和、回声、句中停顿，会抬高打断假阳。
7. **Judge 指标可选且贵。** FDB v1 打断 GPT 分、v1.5 行为 / 韵律 judge 需要额外模型凭证。只跑时序仍然有效；不要把有 judge 和没 judge 的榜混在一起。
8. **中文覆盖不均匀。** 不少论文写 multilingual，只是因为有一个中文子集。声称中文结果前，先核对哪些任务真的翻译了。

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

---

## 贡献

见 [CONTRIBUTING.md](CONTRIBUTING.md)。一句话：补一行时写清 Focus / Protocol / Stimulus / Open / 语言 / 核心指标，并说明这个数字 **不是** 什么。`README.md` 和 `README.zh-CN.md` **两边都要改**。
