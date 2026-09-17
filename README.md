# Awesome Full-Duplex Benchmark [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

**English | [中文](README.zh-CN.md)**

A curated list of **evaluation** resources for full-duplex spoken dialogue: benchmarks, metrics, protocols, challenge sets, and component-level tests.

Models and training data live in the sister list: [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM). This repo is for people who actually run evals.

Welcome to PR if you want to add a benchmark, metric definition, or a note about what a number actually means.

### Legend

**Focus** — what the entry actually measures:

| Focus | Meaning |
|:--|:--|
| **Interaction** | Pause, turn-taking, backchannel, interruption, overlap. |
| **Multi-turn** | Consistency, correction, entity tracking, safety across rounds. |
| **Tool-use** | Function calling under live speech / disfluency. |
| **Temporal** | When to speak, tempo, synchronized simultaneous speech. |
| **Component** | A detector, not a full dialogue system: EOT, interruption, semantic VAD. |
| **Challenge** | Shared task / leaderboard with a frozen protocol. |

**Protocol** — how the system is exercised:

| Protocol | Meaning |
|:--|:--|
| **Replay** | Stream recorded user audio; record model audio; score offline. |
| **Interactive** | Live examiner or two-agent loop (WebRTC / WebSocket). |
| **Offline** | Score existing audio or model outputs; no live API. |
| **Event** | Model emits timestamps / labels on dual-channel speech. |

**Stimulus** — where the user audio comes from:

| Stimulus | Meaning |
|:--|:--|
| **Synthetic** | LLM text + TTS. Scalable, missing human timing/prosody. |
| **Real** | Human-recorded speech, often dual-channel. |
| **Mixed** | Both, or real speech with synthetic overlap inserted. |

**Open** — what has been released:

| Open | Meaning |
|:--|:--|
| **Code + data** | Runnable eval and released audio / labels. |
| **Code** | Public repo; data missing, gated, or not linked. |
| **Data** | Audio / labels public; scoring code thin or absent. |
| **—** | Paper or tech report only. |

**Year** is the year of first public release (arXiv v1, blog, or repo).

---

## Coverage map

Use this table to pick a bench. One row is one protocol, not one GitHub repo. Full-Duplex-Bench v1 / v1.5 / v2 / v3 share a repo but test different things.

| Bench | Pause | Turn | BC | Interrupt | Overlap filter | Multi-turn | Tool | Temporal | Stimulus | ZH | Protocol |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--|
| **Full-Duplex-Bench v1** | ✓ | ✓ | ✓ | ✓ | | | | | Mixed | ✓ | Replay |
| **Full-Duplex-Bench v1.5** | | | ✓ | ✓ | ✓ | | | | Mixed | partial | Replay |
| **Full-Duplex-Bench v2** | | ✓ | | ✓ | | ✓ | | | Interactive | | Interactive |
| **Full-Duplex-Bench v3** | | ✓ | | ✓ | | ✓ | ✓ | | Real | | Replay / agent |
| **FD-Bench** | | | | ✓ | noise | | | | Synthetic | | Replay |
| **MTR-DuplexBench** | | ✓ | ✓ | ✓ | | ✓ | | | Mixed | | Replay + segment |
| **Game-Time** | | | | | | | | ✓ | Synthetic | | Interactive / task |
| **SID-Bench** | | | | ✓ | noise | | | | Real | ✓ | Event |
| **TurnBench** | | EOT | | ✓ | | | | | Real | | Event |
| **Talking Turns** | | ✓ | ✓ | ✓ | | | | | Real | | Offline / predict |
| **HumDial-FDBench** | | | | ✓ | reject | | | | Real | ✓ | Challenge |

Empty cell = not the main claim of that bench, not "impossible".

---

## Contents

- [System-level interaction](#system-level-interaction)
- [Overlap and interruption](#overlap-and-interruption)
- [Interactive multi-turn](#interactive-multi-turn)
- [Tool use and agents](#tool-use-and-agents)
- [Temporal dynamics](#temporal-dynamics)
- [Component-level tests](#component-level-tests)
- [Challenges and leaderboards](#challenges-and-leaderboards)
- [Eval datasets and stimuli](#eval-datasets-and-stimuli)
- [Metric notes](#metric-notes)
- [Surveys](#surveys)
- [Related lists](#related-lists)

---

## System-level interaction

Replay a user waveform into a live system, then score takeover, latency, and (sometimes) response quality. This is the cheapest way to compare commercial realtime APIs with open cascaded stacks.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench** | 2025 | Interaction | Replay | Mixed | Code + data | EN / ZH | TOR, BC frequency / JSD, takeover latency, interruption GPT score | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Site](https://full-duplex-bench.github.io/) |
| **FD-Bench** | 2025 | Interaction | Replay | Synthetic | Code + data | EN | SIRate / SRIRate / EIRate / NIRate, IRD, FSED, WER | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench)/[Dataset](https://huggingface.co/collections/pengyizhou/fd-bench-audio-68674bd6de6feea91ba3ce37) |
| **MTR-DuplexBench** | 2025 | Multi-turn + interaction | Replay + turn segment | Mixed | — | EN | Conversational features, dialogue quality, instruction following, safety | [arXiv](https://arxiv.org/abs/2511.10262) |

v1 tasks: pause handling, backchannel, smooth turn-taking, user interruption. TOR **direction flips by task** — see [Metric notes](#metric-notes).

---

## Overlap and interruption

Speech-on-speech is the actual full-duplex problem. These benches ask whether the model stops, continues, backchannels, or treats the overlap as noise.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v1.5** | 2025 | Overlap | Replay | Mixed | Code + data | EN / ZH* | Behavior labels, stop / response latency, optional prosody | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Semantic-Aware Interruption Detection (SID-Bench)** | 2026 | Component — interruption | Event | Real | Code + data | EN / ZH | FIR, IRL, APT | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **HumDial-FDBench** | 2026 | Challenge — interrupt / reject | Challenge | Real | Code + data | ZH / EN | Interruption, rejection, delay score | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench)/[Dataset](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench)/[Challenge](https://aslp-lab.github.io/HumDial-Challenge/) |

\* FDB-Zh currently ships a subset of v1.5 (user backchannel is the one commonly released). Do not assume full ZH parity with English.

v1.5 overlap scenarios: user interruption, user backchannel, talking to others, background speech. Papers often report two strategies — **responsive** (stop and answer fast) vs **floor-holding** (filter overlap and keep talking). Neither is universally "better"; the bench is descriptive.

---

## Interactive multi-turn

Replay cannot test whether the system stays coherent after it has already spoken. These setups put an examiner (or a turn segmenter) in the loop.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v2** | 2025 | Multi-turn | Interactive | Examiner | Code + data | EN | Turn-taking fluency, instruction following, correction, entity tracking, safety | [arXiv](https://arxiv.org/abs/2510.07838)/[ACL](https://aclanthology.org/2026.acl-short.4)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **MTR-DuplexBench** | 2025 | Multi-turn | Replay + segment | Mixed | — | EN | Per-turn conversational / quality / IF / safety after segmentation | [arXiv](https://arxiv.org/abs/2511.10262) |

FDB-v2 task families: Daily, Correction, Entity Tracking, Safety. Two pacing setups: Fast vs Slow.

---

## Tool use and agents

Full-duplex quality is not only turn-taking. Agents also have to call tools while the user is disfluent.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v3** | 2026 | Tool-use | Replay / agent | Real disfluency | Code + data | EN | Tool F1, argument accuracy, Pass@1, take-turn, interrupt / filler, latency | [arXiv](https://arxiv.org/abs/2604.04847)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Demo](https://daniellin94144.github.io/FDB-v3-demo) |

v3 disfluency tags: filler, pause, hesitation, false start, self-correction. Domains: travel, finance, housing, e-commerce. Self-correction + chained tool calls are the common failure mode.

---

## Temporal dynamics

Most benches score *what* happened after the user stopped. These score *when* the model speaks, including overlapping on purpose.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **Game-Time** | 2025 | Temporal | Interactive / task | Synthetic | Data | EN | Instruction following under timing, tempo, synchronized speech | [arXiv](https://arxiv.org/abs/2509.26388)/[Demo](https://ga642381.github.io/Game-Time)/[Dataset](https://huggingface.co/datasets/gametime-benchmark/gametime) |

---

## Component-level tests

Score a turn detector, endpointer, or interruption head without standing up a full dialogue product. Useful when you are swapping VAD / semantic-turn modules in a cascaded stack.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **TurnBench** | 2026 | Component — EOT + interrupt | Event | Real dual-channel | Code + data | EN | EOT / INT recall, false positives, timing | [arXiv](https://arxiv.org/abs/2608.25218)/[Site](https://turnbench.sesame.com/)/[Github](https://github.com/SesameAILabs/turnbench)/[Blog](https://www.sesame.com/blog/turnbench) |
| **Talking Turns** | 2025 | Component — event predict | Offline | Real | — | EN | Turn change, backchannel, interruption, floor-taking interruption | [arXiv](https://arxiv.org/abs/2503.01174) |
| **SID-Bench** | 2026 | Component — semantic interrupt | Event | Real | Code + data | EN / ZH | FIR, IRL, APT | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **Easy-Turn** | 2025 | Component — turn detection | Event | Mixed | Code | ZH / EN | Turn-taking detection (model paper with eval) | [arXiv](https://arxiv.org/abs/2509.23938)/[Github](https://github.com/ASLP-lab/Easy-Turn)/[Demo](https://aslp-lab.github.io/Easy-Turn/) |
| **TurnSense** | 2025 | Component — EOU | Event | Real | Code + weights | EN / ZH | End-of-utterance detection | [Github](https://github.com/latishab/turnsense)/[Dataset](https://huggingface.co/datasets/latishab/turns-2k) |

TurnBench note: interruption scoring on the **user** channel works for endpointers and cascaded systems. Native full-duplex models that speak while listening need a different interrupt protocol; the authors call this out.

---

## Challenges and leaderboards

Frozen protocol, public ranking, often a hidden test set. Good for a single comparable number; bad if you need to change the metric.

| Title | Year | Focus | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:--|:-:|
| **HumDial-FDBench** (ICASSP 2026 HumDial) | 2026 | Challenge | Challenge | Real dual-channel | Code + data | ZH / EN | Final = 0.4 Interrupt + 0.4 Reject + 0.2 Delay | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench)/[Challenge](https://aslp-lab.github.io/HumDial-Challenge/) |
| **TurnBench leaderboard** | 2026 | Component | Event | Real | Code + data | EN | EOT / INT recall vs FP at a frozen operating point | [Site](https://turnbench.sesame.com/) |

---

## Eval datasets and stimuli

Not training corpora. These are the audio sources benches actually stream or annotate.

| Title | Year | Used by | Open | Notes | Resources |
|:--|:-:|:--|:-:|:--|:-:|
| **CANDOR** | 2023 | FDB v1 pause / turn-taking | Data | Real two-party conversations; FDB slices pauses and smooth turns | [Paper](https://www.pnas.org/doi/10.1073/pnas.2218522120) |
| **ICC** (In Conversation Corpus) | 2024 | FDB v1 backchannel | Data | Multi-listener backchannel timing; FDB uses TOR / frequency / JSD against this distribution | [Umair et al.](https://arxiv.org/abs/2402.02889) |
| **FDB synthetic sets** | 2025 | FDB v1 interruption / pause | Code + data | TTS user audio with controlled pauses and barge-in | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Full-Duplex-Bench-zh** | 2025 | FDB v1 / partial v1.5 | Data | Chinese replay sets; subset coverage ≠ English | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **TURNS-2K** | 2025 | TurnSense | Data | EOU labels | [Hugging Face](https://huggingface.co/datasets/latishab/turns-2k) |
| **HumDial-FDBench audio** | 2026 | HumDial challenge | Data | Dual-channel real conversations with overlap | [Hugging Face](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench) |
| **TurnBench conversations** | 2026 | TurnBench | Data | ~30 h studio dual-channel, 6 conversation types, 3-annotator EOT / INT | [Viewer](https://turnbench.sesame.com/conversations) |
| **Game-Time tasks** | 2025 | Game-Time | Data | Timing / tempo / sync game-like tasks | [Hugging Face](https://huggingface.co/datasets/gametime-benchmark/gametime) |

Training-scale duplex corpora (DuplexChat, DuplexGen, SmoothConv, SOMMELIER, …) stay on the [model-centric list](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM#datasets).

---

## Metric notes

These are the details that make two papers incomparable if you ignore them.

1. **TOR is not one number.** In FDB v1, takeover rate is **lower-better** on pause handling and **higher-better** on smooth turn-taking and user interruption. Always write the task next to TOR.
2. **FDB backchannel rule.** Official code treats a response as backchannel when duration < 1 s **and** word count ≤ 3. Short audible leaks that fail this rule still count as takeovers. If you care about "did the model make any sound during a pause", add a stricter energy-based rate.
3. **Latency denominators differ.** Some benches average latency over all samples; FDB turn-taking latency is usually only on takeover samples. SID-Bench's APT folds false interrupts and slow interrupts into one penalty.
4. **Product VAD is part of the system.** Matching every API to the same `silence_duration_ms` is not "fairer"; it is a different product. Report the shipped default (or the knob you actually set) next to the score.
5. **Replay ≠ conversation.** Replay benches cannot test whether the model's own speech causes the next user event. FDB-v2 / Game-Time / human challenges close that loop; they also cost more and drift with examiner models.
6. **Synthetic overlap is clean.** TTS barge-in has sharp onsets and little bleed. Real dual-channel sets (TurnBench, HumDial, SID-Bench) have backchannels, echo, and mid-turn pauses that inflate interruption false positives.
7. **Judge metrics are optional and expensive.** FDB v1 interruption GPT scores and v1.5 behavior / prosody judges need extra model credentials. Timing-only runs are still valid; do not mix judged and unjudged leaderboards.
8. **ZH coverage is uneven.** Many papers list "multilingual" because one Chinese subset exists. Check which tasks are actually translated before claiming a Chinese result.

---

## Surveys

| Title | Year | Why it matters for eval | Resources |
|:--|:-:|:--|:-:|
| **A Survey of Full-Duplex Spoken Dialogue Systems: Architectural Hierarchy, Interaction Ontology, and Decision State Machine** | 2026 | Interaction ontology and decision states — useful when you name what a metric is supposed to capture | [arXiv](https://arxiv.org/abs/2606.19453)/[Github](https://github.com/DuplexLM/DuplexSurvey) |
| **From Turn-Taking to Synchronous Dialogue: A Survey of Full-Duplex Spoken Language Models** | 2025 | Maps half-duplex vs full-duplex eval gaps | [arXiv](https://arxiv.org/abs/2509.14515)/[Github](https://github.com/elpsykongloo/FD-SLMs) |

---

## Related lists

- [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM) — models, components, training datasets.
- [Full-Duplex-Bench](https://github.com/DanielLin94144/Full-Duplex-Bench) — the main open eval suite (v1 / v1.5 / v2 / v3).

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Short version: add a row with Focus / Protocol / Stimulus / Open / Lang / headline metrics, and say what the number is *not*. Update **both** `README.md` and `README.zh-CN.md`.
