# Timing

**[Index](README.md) · [中文](timing.zh-CN.md)**

This class scores **how fast and on what rhythm**. A system can be fast and still barge in on pauses. Timing is not a substitute for [Interaction](interaction.md).

```
user speaking | user stops | you start | you speaking | user barges in | you stop
              |← Response / First audio →|            |← Stop latency →|
```

## Subclasses

| Subclass | Clock starts | Clock stops | What it asks | Typical benches |
|:--|:--|:--|:--|:--|
| **Response latency** | User yielded the floor | You start speaking | Are you slow to take a real turn? | FDB v1 takeover latency, HumDial delay, τ-Voice |
| **Stop latency** | User starts an interrupt | You go silent | After a barge-in, how long until you shut up? | FDB v1.5 stop latency, SID IRL |
| **First audio** | The system is allowed to generate | First audible frame / first packet | Pipeline delay (VAD → model → TTS → net), not “will you take the turn” | Product TTFB; parts of FDB v3 |
| **Tempo** | A time structure the task imposes | Whether you hit it | Rate, deadlines, intentional overlap / sync | Game-Time |

**Response** vs **First audio**: response is dialogue time (user EOT → mouth). First audio is system time (request → first PCM). Users often hear First audio as “slow” even when Interaction TOR looks fine.

**Denominators differ.** FDB turn-taking latency is usually averaged only on takeover samples. Averaging silent trials as well is a different number. SID APT folds false interrupts and slow interrupts into one penalty.

Do not merge Timing with Interaction into one “latency score”.
