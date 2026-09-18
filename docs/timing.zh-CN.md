# 时序

**[目录](README.zh-CN.md) · [English](timing.md)**

这一类打的是 **快慢和节奏**。一个系统可以很快，同时很爱在停顿上误抢。时序不能代替 [交互](interaction.zh-CN.md)。

```
用户还在说 | 用户停 | 你开口 | 你在说 | 用户抢话 | 你停
           |← 接话 / 首音 →|        |← 停话时延 →|
```

## 小类

| 小类 | 起点 | 终点 | 在问什么 | 典型 bench |
|:--|:--|:--|:--|:--|
| **Response latency** | 用户该交轮了 | 你开口 | 该接的时候慢不慢 | FDB v1 takeover 时延、HumDial delay、τ-Voice |
| **Stop latency** | 用户开始抢话 | 你静音 | 被打断后多久把音停掉 | FDB v1.5 stop latency、SID IRL |
| **First audio** | 系统可以开始生成 | 第一帧可听 / 首包 | 链路时延（VAD → 模型 → TTS → 网络），不是「会不会接话」 | 产品 TTFB；FDB v3 的一部分 |
| **Tempo** | 任务规定的时间结构 | 有没有踩上 | 语速、限时、故意叠说 / 同步 | Game-Time |

**接话** vs **首音**：接话是对话时钟（用户 EOT → 开口）。首音是系统时钟（请求 → 第一帧 PCM）。交互 TOR 好看时，听感慢往往是首音。

**分母不一样。** FDB 轮次时延通常只在 takeover 样本上平均。把没开口的也算进去是另一个数。SID 的 APT 把误打断和慢打断折在一起。

不要把时序和交互合成一个「latency 总分」。
