# 任务与工具

**[目录](README.zh-CN.md) · [English](task.md)**

这一类打的是 **用户还在说话时把事办成** — 工具、参数、多步调用、不流畅。纯闲聊应标 **N/A**，不要打 0。

[内容](content.zh-CN.md) 的 Instruction 问「还在不在办这件事」。Task 问「API / 数据库 / 政策这一步有没有做对」。工具 bench 上的 [交互](interaction.zh-CN.md) 接话率只是旁证，不是 Task 分。

## 小类

| 小类 | 在问什么 | 典型错法 |
|:--|:--|:--|
| **Tool select** | 调对了哪个函数 / API | 看起来像、其实调错 |
| **Args** | 从语音里填对槽位 | ASR 一糊就丢日期、换城市 |
| **Chain** | 多步调用还能对上 | 第一步对，第二步用了过期 id；Pass@1 直接挂 |
| **Disfluency** | 填充词、停顿、犹豫、假开始、自我修正下仍然对 | 把改口当成第二个意图，调两次 |

目前公开的全双工工具 bench 主要是 FDB v3（真人 disfluency，四个领域）。τ-Voice（接地客服工具 + 全双工用户模拟）也是这一类的主论文，主表里还没单独成行。

VoiceAgentBench / AudioCRAG 会调工具，但不考全双工抢话。文本 τ-bench / BFCL 不进这个列表。
