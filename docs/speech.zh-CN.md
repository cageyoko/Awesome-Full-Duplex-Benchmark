# 语音与稳健

**[目录](README.zh-CN.md) · [English](speech.md)**

这一类打的是 **音频能不能用**。论文覆盖薄，产品报告里仍应占一格。

它不是 [交互](interaction.zh-CN.md)（该不该说），也不是 [时序](timing.zh-CN.md)（何时说）。停得及时的模型仍可能听不清，或说到一半掉线。

## 小类

| 小类 | 在问什么 | 现在有什么 |
|:--|:--|:--|
| **Intelligibility** | 人 / ASR 能不能听清模型语音 | FD-Bench 对模型音频的 WER。没有独立的全双工可懂度集 |
| **Prosody** | 重叠之后音量、语速、切停像不像人 | FDB v1.5 可选韵律 judge |
| **Noise** | 背景音、回声、串音 | SID 噪声/静音；FD-Bench NIRate。真人双通道比 TTS 抢话狠 |
| **Stability** | 无响应、卡死、播到一半掉线 | 几乎没有论文 bench。对比 API 时仍应报 |

Judge / MOS 需要额外凭证。不要把有 judge 的 Speech 行和只跑时序的交互榜混在一起。
