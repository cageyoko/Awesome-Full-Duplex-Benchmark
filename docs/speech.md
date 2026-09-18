# Speech

**[Index](README.md) · [中文](speech.zh-CN.md)**

This class scores **whether the audio is usable**. Papers under-cover it; a product report still needs the row.

It is not [Interaction](interaction.md) (should you speak) and not [Timing](timing.md) (when). A model that stops on time can still be unintelligible or die mid-utterance.

## Subclasses

| Subclass | What it asks | What exists today |
|:--|:--|:--|
| **Intelligibility** | Can a person / ASR hear the model speech? | FD-Bench WER on **model** audio. AA-WER (`VoxPopuli-Cleaned-AA`, `Earnings22-Cleaned-AA`, held-out AgentTalk) is **user/ASR** transcription, a different object |
| **Prosody** | After overlap, does volume / rate / cut-off sound human? | Optional FDB v1.5 prosody judge |
| **Noise** | Background speech, echo, channel bleed | SID noise/silence; FD-Bench NIRate. Real dual-channel is harsher than TTS barge-in |
| **Stability** | No-response, hang, dropout mid-stream | Almost no paper bench. Report it anyway when comparing APIs |

Judge / MOS numbers need extra credentials. Do not mix judged Speech rows with timing-only Interaction leaderboards.
