# 如何贡献

**[English](CONTRIBUTING.md) | 中文**

这个列表只收 **评测**。一篇模型论文里附带两页「我们也报了 TOR」，应放到 [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM)，不要放这里 — 除非它给出了别人能复用的协议、数据或指标定义。

章节按 **打什么分** 排，不按仓库或会议：

1. 交互控制
2. 时序
3. 多轮内容
4. 任务与工具
5. 语音与稳健

`Component` 和 `Challenge` 是标签（粒度 / 协议），不是章节。同一篇论文可以出现在多个大类。语音问答或半双工工具 bench 放进 **相邻**，不要开第六大类。

## 增改条目

1. 开 PR 时必须同时改 **`README.md`（英文）和 `README.zh-CN.md`（中文）**，两边保持同步。如果改了某个大类或小类的定义，同步改 `docs/` 里对应的 `*.md` 和 `*.zh-CN.md`。
2. 条目放进 **实际被打分的那个大类**，不要按会议或 GitHub 仓库归堆。若它在第二个大类也是主声称，就再写一行（例如 FDB v1 同时出现在交互和时序；τ-Voice 同时出现在任务和交互）。
3. 填齐 Class / Subclass、Granularity、Protocol、Stimulus（`Synthetic` / `Real` / `Mixed` / `Text`）、Open（`Code + data` / `Code + weights` / `Code` / `Data` / `—`）。不确定就写 `—` 或 `?`，不要编。这些标签两边都保留英文。没有放出对应语种评测集，就不要写 `ZH / EN`。
4. 有 arXiv / 会议、代码、数据、demo 就链上。只有论文 PDF 的 GitHub 不要链。
5. **核心指标** 写短名，方向不明显时标 ↑/↓。TOR 随小类翻转时必须写明。
6. 如果你跑过这个 bench，在 [指标注意事项](README.zh-CN.md#指标注意事项) / [Metric notes](README.md#metric-notes) 加一句 caveat，比在标题里再加形容词有用。
7. 主声称变了，两边 README 的覆盖图都要改。
8. 厂商发版博主打的集变了，同步改 `docs/commercial.md` 和 `docs/commercial.zh-CN.md`。没有可复跑协议的博客分数，不要抄进覆盖图。

## 建议的 PR 标题

`Add <BenchName> (<year>)` 或 `Fix <BenchName> class / links`。

## 不会合并的

- 同一个大类里的重复行（改旧的）。
- 再开一个 Component 或 Challenge 章节。
- 只有训练、没有评测划分或打分脚本的数据。
- 没有可复跑 / 可引用协议的闭源产品博客。
- 没有指标定义的营销榜。
- 把 Interaction 小类平均成一个标量。

## 本地预览

GitHub 渲染 `README.md` / `README.zh-CN.md` 就是预览。
