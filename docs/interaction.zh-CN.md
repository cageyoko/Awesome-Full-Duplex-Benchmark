# 交互控制

**[目录](README.zh-CN.md) · [English](interaction.md)**

这一类打的是 **何时说、何时停、何时不说**。不打话说得对不对（那是 [内容](content.zh-CN.md) / [任务](task.zh-CN.md)），也不打动作花了多少毫秒（那是 [时序](timing.zh-CN.md)）。

**不要**把这些小类平均成一个 TOR：停顿要少抢，接话要多接。

模型正在说、用户通道里突然有声音：

```
是对你说的吗？
  ├─ 不是 / 不是话              → Filter
  ├─ 是，但不抢轮（嗯、对）      → Backchannel
  └─ 是，并且要轮                → Interrupt

Reject = 「正确否定」的打分桶
          （常常装 Filter + 用户附和 + 假打断）
```

## 小类

| 小类 | 发生了什么 | 系统该怎样 | 典型错法 |
|:--|:--|:--|:--|
| **Pause** | 句中停顿，用户没说完 | 继续听，别抢 | 把空隙当轮次结束 |
| **Turn** | 用户说完，地板空了 | 接话 | 不接，或接得太早 |
| **Backchannel** | 短附和。仍是对你说的，但不抢地板 | 用户嗯一声：你继续说。该你嗯时：只出短音，不要开成长轮 | 把「嗯」当打断；或只该嗯时讲了一大段 |
| **Interrupt** | 你还在说，用户要轮 | 停下，再接新意图 | 把旧句子念完 |
| **Filter** | 旁人说话、电视、噪声 — 不是对你说的 | 当没听到 | 回答噪声 |
| **Reject** | HumDial 那种「这段重叠不算合法打断」 | 不接管 | 误接受。和 Filter、用户附和重叠；不是第四种用户行为 |

附和有两个方向。FDB v1 的 ICC 问的是 *系统* 会不会在 TRP 上嗯。FDB v1.5 的用户附和问的是 *系统* 会不会在用户只嗯了一声时误停。

## 出现在哪些 bench

FDB v1（停顿 / 轮次 / 附和 / 打断）、FDB v1.5（打断 / 附和 / 过滤）、FD-Bench、HumDial（打断 / 拒识）、SID-Bench、TurnBench、Talking Turns、Easy-Turn（complete / incomplete / backchannel / wait）、τ-Voice（响应率 / 打断率 / 选择性）。

TOR 方向和 FDB 附和规则（`< 1 秒` 且 `≤ 3` 词）见 [指标注意事项](../README.zh-CN.md#指标注意事项)。
