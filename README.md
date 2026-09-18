# Awesome Full-Duplex Benchmark [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

**English | [中文](README.zh-CN.md)**

A curated list of **evaluation** resources for full-duplex spoken dialogue, arranged as a final report card: what to score, not which GitHub repo to clone.

Models and training data live in the sister list: [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM). This repo is for people who actually run evals.

Welcome to PR if you want to add a benchmark, metric definition, or a note about what a number actually means.

### Legend

**Class** — what the score is about. Protocol and venue are not classes. Each class has a short note under [`docs/`](docs/README.md).

| Class | Subclass | Meaning |
|:--|:--|:--|
| **[Interaction](docs/interaction.md)** | Pause / Turn / Backchannel / Interrupt / Filter / Reject | When to speak, stop, or stay silent. |
| **[Timing](docs/timing.md)** | Response latency / Stop latency / First audio / Tempo | How fast and on what rhythm. Not the same as being correct. |
| **[Content](docs/content.md)** | Instruction / Correction / Entity / Post-interrupt / Safety | Whether the words are right after the system has already spoken or been cut off. |
| **[Task](docs/task.md)** | Tool select / Args / Chain / Disfluency | Getting work done while the user is talking. Idle-chat systems may mark this N/A. |
| **[Speech](docs/speech.md)** | Intelligibility / Prosody / Noise / Stability | Whether the audio is usable. Papers under-cover this; products cannot. |

**How** — how the system is exercised. These are columns, not sections.

| Tag | Values | Meaning |
|:--|:--|:--|
| **Granularity** | System / Component | Full dialogue product vs a detector (EOT, interruption, semantic VAD). |
| **Protocol** | Replay / Interactive / Offline / Event / Challenge | Stream recorded audio; live examiner; score existing outputs; emit timestamps; frozen shared task. |
| **Stimulus** | Synthetic / Real / Mixed / Text | TTS; human (often dual-channel); both; STT/transcript turns with no waveform. |
| **Open** | Code + data / Code + weights / Code / Data / — | What was released. `—` = paper only. |

**Year** is the year of first public release (arXiv v1, blog, or repo).

A paper may appear in more than one class. Full-Duplex-Bench v1 / v1.5 / v2 / v3 share a repo and are different protocols.

---

## Coverage map

One row is one protocol. Empty cell = not the main claim, not "impossible".

| Bench | Pause | Turn | BC | Int | Filter | Reject | Lat | Tempo | Content | Task | Speech | Granularity | Protocol | ZH |
|:--|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| **Full-Duplex-Bench v1** | ✓ | ✓ | ✓ | ✓ | | | ✓ | | post-int. | | | System | Replay | ✓ |
| **Full-Duplex-Bench v1.5** | | | ✓ | ✓ | ✓ | | ✓ | | | | prosody* | System | Replay | partial |
| **Full-Duplex-Bench v2** | | ✓ | | ✓ | | | | | ✓ | | | System | Interactive | |
| **Full-Duplex-Bench v3** | | ✓ | | ✓ | | | ✓ | | | ✓ | | System | Replay | |
| **FD-Bench** | | | | ✓ | noise | | ✓ | | | | WER | System | Replay | |
| **MTR-DuplexBench** | | ✓ | ✓ | ✓ | | | | | ✓ | | | System | Replay + segment | |
| **Game-Time** | | | | | | | | ✓ | | | | System | Interactive | |
| **SID-Bench** | | | | ✓ | noise | | ✓ | | | | | Component | Event | ✓ |
| **TurnBench** | | EOT | | ✓ | | | ✓ | | | | | Component | Event | |
| **Talking Turns** | | ✓ | ✓ | ✓ | | | | | | | | Component | Offline | |
| **HumDial-FDBench** | | | | ✓ | | ✓ | ✓ | | | | | System | Challenge | ✓ |
| **Easy-Turn** | | ✓ | ✓ | ✓ | | | | | | | | Component | Event | ✓ |
| **TurnSense** | | EOU | | | | | | | | | | Component | Offline | |
| **τ-Voice** | | ✓ | ✓ | ✓ | ✓ | | ✓ | | | ✓ | | System | Interactive | |
| **Audio MultiChallenge** | | | | | | | | | ✓ | | | System | Offline | |

\* Optional judge. Timing-only v1.5 runs are still valid.

---

## Contents

- [1. Interaction control](#1-interaction-control) · [note](docs/interaction.md)
- [2. Timing](#2-timing) · [note](docs/timing.md)
- [3. Multi-turn content](#3-multi-turn-content) · [note](docs/content.md)
- [4. Task and tools](#4-task-and-tools) · [note](docs/task.md)
- [5. Speech and robustness](#5-speech-and-robustness) · [note](docs/speech.md)
- [Adjacent: spoken understanding and half-duplex agents](#adjacent-spoken-understanding-and-half-duplex-agents)
- [Commercial API evals](docs/commercial.md) · which sets GPT / Gemini / Grok / Seed / Qwen headline
- [Eval datasets and stimuli](#eval-datasets-and-stimuli)
- [Metric notes](#metric-notes)
- [Surveys](#surveys)
- [Related lists](#related-lists)

---

## 1. Interaction control

When to speak, when to stop, when not to speak. Do **not** average these subclasses into one TOR: pause wants fewer takeovers, turn-taking wants more.

| Title | Year | Subclass | Granularity | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v1** | 2025 | Pause / Turn / Backchannel / Interrupt | System | Replay | Mixed | Code + data | EN / ZH | TOR (direction flips by task), BC frequency / JSD, takeover latency, interruption GPT score | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Site](https://full-duplex-bench.github.io/) |
| **Full-Duplex-Bench v1.5** | 2025 | Interrupt / Backchannel / Filter | System | Replay | Mixed | Code + data | EN / ZH* | Behavior labels, stop / response latency, optional prosody | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **FD-Bench** | 2025 | Interrupt / Filter | System | Replay | Synthetic | Code + data | EN | SIRate / SRIRate / EIRate / NIRate, IRD, FSED, WER | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench)/[Dataset](https://huggingface.co/collections/pengyizhou/fd-bench-audio-68674bd6de6feea91ba3ce37) |
| **HumDial-FDBench** | 2026 | Interrupt / Reject | System | Challenge | Real | Code + data | ZH / EN | Interrupt, reject, delay; Final = 0.4 / 0.4 / 0.2 | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench)/[Dataset](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench)/[Challenge](https://aslp-lab.github.io/HumDial-Challenge/) |
| **SID-Bench** | 2026 | Interrupt / Filter | Component | Event | Real | Code + data | EN / ZH | FIR, IRL, APT | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **TurnBench** | 2026 | Turn (EOT) / Interrupt | Component | Event | Real | Code + data | EN | EOT / INT recall, false positives, timing; public leaderboard | [arXiv](https://arxiv.org/abs/2608.25218)/[Site](https://turnbench.sesame.com/)/[Github](https://github.com/SesameAILabs/turnbench)/[Blog](https://www.sesame.com/blog/turnbench) |
| **Talking Turns** | 2025 | Turn / Backchannel / Interrupt | Component | Offline | Real | — | EN | Turn change, backchannel, interruption, floor-taking interruption. Eval platform promised; no public scorer found. | [arXiv](https://arxiv.org/abs/2503.01174)/[Apple](https://machinelearning.apple.com/research/talking-turns) |
| **Easy-Turn** | 2025 | Turn / Backchannel / Interrupt | Component | Event | Mixed | Code + data | ZH / EN | Four-state detector (complete / incomplete / backchannel / wait) on its own testset, not a system replay bench | [arXiv](https://arxiv.org/abs/2509.23938)/[Github](https://github.com/ASLP-lab/Easy-Turn)/[Demo](https://aslp-lab.github.io/Easy-Turn/) |
| **TurnSense** (latishab) | 2025 | Turn (EOU) | Component | Offline | Text | Code + weights | EN | Text-level EOU on TURNS-2K. Not Bairong/brgroup TurnSense (ZH/EN audio). | [Github](https://github.com/latishab/turnsense)/[Dataset](https://huggingface.co/datasets/latishab/turns-2k) |
| **τ-Voice** | 2026 | Turn / Interrupt / Backchannel / Filter | System | Interactive | Mixed | Code + data | EN | Responsiveness, interrupt rate, selectivity (ignore BC / side talk). Interaction is scored, but pass@1 is the Task number. | [arXiv](https://arxiv.org/abs/2603.13686)/[Github](https://github.com/sierra-research/tau2-bench)/[Blog](https://sierra.ai/blog/tau-voice-benchmarking-real-time-voice-agents-on-real-world-tasks) |

\* FDB-Zh currently ships a subset of v1.5 (user backchannel is the one commonly released). Do not assume full ZH parity with English.

v1.5 overlap scenes: user interruption, user backchannel, talking to others, background speech. Papers often report **responsive** (stop and answer) vs **floor-holding** (filter overlap and keep talking). Neither is universally better; the bench is descriptive.

TurnBench interruption scoring on the **user** channel works for endpointers and cascaded systems. Native full-duplex models that speak while listening need a different interrupt protocol.

Also reports interaction signals: [FDB v3](#4-task-and-tools) (take-turn / interrupt), [MTR-DuplexBench](#3-multi-turn-content) (conversational features), [τ-Voice](#4-task-and-tools) (interrupt rate / selectivity).

---

## 2. Timing

How fast, and on what rhythm. A system can be fast and still barge in on pauses.

| Title | Year | Subclass | Granularity | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Game-Time** | 2025 | Tempo | System | Interactive | Synthetic | Data | EN | Instruction following under timing, tempo, synchronized speech | [arXiv](https://arxiv.org/abs/2509.26388)/[Demo](https://ga642381.github.io/Game-Time)/[Dataset](https://huggingface.co/datasets/gametime-benchmark/gametime) |
| **Full-Duplex-Bench v1** | 2025 | Response latency | System | Replay | Mixed | Code + data | EN / ZH | Takeover latency, usually on takeover samples only | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Full-Duplex-Bench v1.5** | 2025 | Stop / response latency | System | Replay | Mixed | Code + data | EN / ZH* | Stop and response latency under overlap | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **FD-Bench** | 2025 | Response / stop latency | System | Replay | Synthetic | Code + data | EN | IRD, FSED, ERT, EIT | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench) |
| **SID-Bench** | 2026 | Stop latency | Component | Event | Real | Code + data | EN / ZH | IRL; APT folds false and slow interrupts | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |
| **HumDial-FDBench** | 2026 | Response latency | System | Challenge | Real | Code + data | ZH / EN | Delay score (0.2 of Final) | [arXiv](https://arxiv.org/abs/2604.21406)/[Github](https://github.com/ASLP-lab/HumDial-FDBench) |
| **Full-Duplex-Bench v3** | 2026 | Response / first audio | System | Replay | Real | Code + data | EN | First-word, tool-call, and task-completion latency | [arXiv](https://arxiv.org/abs/2604.04847)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **τ-Voice** | 2026 | Response latency | System | Interactive | Mixed | Code + data | EN | Voice-interaction latency under Clean vs Realistic | [arXiv](https://arxiv.org/abs/2603.13686)/[Github](https://github.com/sierra-research/tau2-bench) |

First-audio / first-packet latency is a product metric. Almost no paper treats it as a first-class bench; still report it when comparing APIs.

---

## 3. Multi-turn content

Whether the words stay right after the system has spoken, been interrupted, or been corrected. Replay cannot fully test this. Idle interaction TOR does not substitute.

| Title | Year | Subclass | Granularity | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v2** | 2025 | Instruction / Correction / Entity / Safety | System | Interactive | Mixed | Code + data | EN | Turn-taking fluency, instruction following, correction, entity tracking, safety | [arXiv](https://arxiv.org/abs/2510.07838)/[ACL](https://aclanthology.org/2026.acl-short.4)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **MTR-DuplexBench** | 2025 | Instruction / Safety (+ dialogue quality) | System | Replay + segment | Mixed | — | EN | Per-turn conversational / quality / IF / safety after segmentation | [arXiv](https://arxiv.org/abs/2511.10262) |
| **Full-Duplex-Bench v1** | 2025 | Post-interrupt | System | Replay | Mixed | Code + data | EN / ZH | Interruption GPT score (optional judge) | [arXiv](https://arxiv.org/abs/2503.04721)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Audio MultiChallenge** | 2025 | Instruction / Correction / Entity | System | Offline | Real | Data | EN | Rubric pass rate: Inference Memory, Instruction Retention, Self Coherence, Voice Editing (mid-utterance repair) | [arXiv](https://arxiv.org/abs/2512.14865)/[ACL](https://aclanthology.org/2026.acl-long.1654/)/[Dataset](https://huggingface.co/datasets/ScaleAI/audiomc)/[Leaderboard](https://scale.com/leaderboard/audiomc) |

FDB-v2 task families: Daily, Correction, Entity Tracking, Safety. Two pacing setups: Fast vs Slow.

Audio MultiChallenge is multi-turn **context**, then one scored response — Offline, not a live examiner. Voice Editing is Correction; Audio-Cue memory is Entity, not Interaction TOR.

---

## 4. Task and tools

Getting work done while the user is disfluent. Chat-only systems should mark this **N/A**, not zero.

| Title | Year | Subclass | Granularity | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **Full-Duplex-Bench v3** | 2026 | Tool select / Args / Chain / Disfluency | System | Replay | Real disfluency | Code + data | EN | Tool F1, argument accuracy, Pass@1, take-turn, interrupt / filler, latency | [arXiv](https://arxiv.org/abs/2604.04847)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench)/[Demo](https://daniellin94144.github.io/FDB-v3-demo) |
| **τ-Voice** | 2026 | Tool select / Args / Chain / Disfluency | System | Interactive | Mixed | Code + data | EN | pass@1 vs text τ²-bench (278 retail / airline / telecom tasks); Clean vs Realistic (noise / accent / turn-taking) | [arXiv](https://arxiv.org/abs/2603.13686)/[Github](https://github.com/sierra-research/tau2-bench)/[Blog](https://sierra.ai/blog/tau-voice-benchmarking-real-time-voice-agents-on-real-world-tasks) |

v3 disfluency tags: filler, pause, hesitation, false start, self-correction. Domains: travel, finance, housing, e-commerce. Self-correction + chained tool calls are the common failure mode.

τ-Voice reuses τ²-bench tools, policies, and database checks. The Task number is pass@1. Interrupt rate / selectivity belong in Interaction; latency belongs in Timing. Text-only τ-bench / BFCL stay off this list.

Gemini blogs also cite a closed **ComplexFuncBench Audio** function-calling set. The public [ComplexFuncBench](https://github.com/zai-org/ComplexFuncBench) is text; the audio variant is not a rerunnable protocol here.

---

## 5. Speech and robustness

Whether the audio is usable. This class is thin in the literature and should still appear on a final report.

| Title | Year | Subclass | Granularity | Protocol | Stimulus | Open | Lang | Headline metrics | Resources |
|:--|:-:|:--|:-:|:-:|:-:|:-:|:-:|:--|:-:|
| **FD-Bench** | 2025 | Intelligibility / Noise | System | Replay | Synthetic | Code + data | EN | WER; NIRate on noise gaps | [arXiv](https://arxiv.org/abs/2507.19040)/[Github](https://github.com/pengyizhou/FD-Bench) |
| **Full-Duplex-Bench v1.5** | 2025 | Prosody | System | Replay | Mixed | Code + data | EN / ZH* | Optional prosody adaptation under overlap | [arXiv](https://arxiv.org/abs/2507.23159)/[Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **SID-Bench** | 2026 | Noise | Component | Event | Real | Code + data | EN / ZH | Noise / silence APT and FIR | [arXiv](https://arxiv.org/abs/2603.24144)/[Github](https://github.com/xkx-hub/SID-bench) |

Still missing as first-class public benches: echo / channel bleed, no-response rate, dropouts, and a standalone intelligibility set for model speech. Product evals should add them even when the paper list cannot.

---

## Adjacent: spoken understanding and half-duplex agents

These score **speech-in content or tools**, not full-duplex floor control. GPT Realtime / Gemini Live numbers often appear here. Do not mix them with Interaction TOR. Which set each vendor *headlines* is on [Commercial API evals](docs/commercial.md).

| Title | Year | What is scored | Why adjacent | Open | Lang | Resources |
|:--|:-:|:--|:--|:-:|:-:|:--|
| **VoiceBench** | 2024 | Knowledge, instruction following, safety under accent / reverb | Speech-in QA; no overlap protocol | Code + data | EN | [arXiv](https://arxiv.org/abs/2410.17196)/[Github](https://github.com/MatthewCYM/VoiceBench) |
| **WildSpeech-Bench** | 2025 | Single-turn S2S content, paralinguistics, noise | Real spoken queries; still one-shot, not duplex | Code + data | EN | [arXiv](https://arxiv.org/abs/2506.21875)/[Github](https://github.com/Tencent/WildSpeech-Bench)/[Dataset](https://huggingface.co/datasets/tencent/WildSpeech-Bench) |
| **VocalBench** | 2025 | Response quality, acoustics, conversational flow | Half-duplex vocal conversation; has a ZH split | Code + data | EN / ZH | [arXiv](https://arxiv.org/abs/2505.15727)/[Github](https://github.com/SJTU-OmniAgent/VocalBench)/[ZH](https://github.com/SJTU-OmniAgent/VocalBench-zh) |
| **VoiceAgentBench** | 2025 | Tool select / args / chain / safety | Spoken tools, no barge-in scoring | Code + data | EN + Indic | [arXiv](https://arxiv.org/abs/2510.07978)/[Github](https://github.com/ola-krutrim/VoiceAgentBench)/[Dataset](https://huggingface.co/datasets/krutrim-ai-labs/VoiceAgentBench) |
| **AudioCRAG** | 2025 | Spoken factual QA with web / KG tools | Spoken RAG (from Stream RAG); not floor control | Data | EN | [arXiv](https://arxiv.org/abs/2510.02044) |

---

## Eval datasets and stimuli

Not training corpora. These are the audio sources benches actually stream or annotate.

| Title | Year | Used by | Open | Notes | Resources |
|:--|:-:|:--|:-:|:--|:-:|
| **CANDOR** | 2023 | FDB v1 pause / turn | Data | Real two-party English video-chat conversations (Science Advances, not PNAS); FDB slices pauses and smooth turns | [Paper](https://www.science.org/doi/10.1126/sciadv.adf3197) |
| **ICC** (In Conversation Corpus) | 2024 | FDB v1 backchannel | Data | Multi-listener backchannel timing on 55 ICC turns. Full ICC is IRB-restricted; FDB uses the released backchannel responses | [Umair et al.](https://arxiv.org/abs/2410.16044)/[ACL](https://aclanthology.org/2024.findings-emnlp.909/) |
| **FDB synthetic sets** | 2025 | FDB v1 interruption / pause | Code + data | TTS user audio with controlled pauses and barge-in | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **Full-Duplex-Bench-zh** | 2025 | FDB v1 / partial v1.5 | Data | Chinese replay sets; subset coverage ≠ English | [Github](https://github.com/DanielLin94144/Full-Duplex-Bench) |
| **TURNS-2K** | 2025 | TurnSense (latishab) | Data | 2k English **text** turns with binary EOU labels, not waveform | [Hugging Face](https://huggingface.co/datasets/latishab/turns-2k) |
| **Easy Turn testset** | 2025 | Easy-Turn | Data | 800 clips: complete/incomplete 300 each, backchannel/wait 100 each; real + TTS, human-labeled states | [Github](https://github.com/ASLP-lab/Easy-Turn) |
| **HumDial-FDBench audio** | 2026 | HumDial | Data | Dual-channel real conversations with overlap | [Hugging Face](https://huggingface.co/datasets/ASLP-lab/HumDial-FDBench) |
| **TurnBench conversations** | 2026 | TurnBench | Data | ~30 h studio dual-channel, 6 conversation types, 3-annotator EOT / INT | [Viewer](https://turnbench.sesame.com/conversations) |
| **Game-Time tasks** | 2025 | Game-Time | Data | Timing / tempo / sync game-like tasks | [Hugging Face](https://huggingface.co/datasets/gametime-benchmark/gametime) |
| **Audio MultiChallenge** | 2025 | Audio MultiChallenge | Data | 452 real multi-turn conversations, 47 speakers, 1,712 rubrics | [Hugging Face](https://huggingface.co/datasets/ScaleAI/audiomc) |
| **τ²-bench tasks** | 2025 | τ-Voice | Code + data | 278 retail / airline / telecom tool tasks; voice layer is a simulator, not a static waveform set | [Github](https://github.com/sierra-research/tau2-bench) |

Training-scale duplex corpora (DuplexChat, DuplexGen, SmoothConv, SOMMELIER, …) stay on the [model-centric list](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM#datasets).

---

## Metric notes

These are the details that make two papers incomparable if you ignore them.

1. **TOR is not one number.** In FDB v1, takeover rate is **lower-better** on pause handling and **higher-better** on smooth turn-taking and user interruption. Always write the subclass next to TOR. Do not average Interaction into a single score.
2. **FDB backchannel rule.** Official code treats a response as backchannel when duration < 1 s **and** word count ≤ 3. Short audible leaks that fail this rule still count as takeovers. If you care about "did the model make any sound during a pause", add a stricter energy-based rate.
3. **Latency denominators differ.** Some benches average latency over all samples; FDB turn-taking latency is usually only on takeover samples. SID-Bench's APT folds false interrupts and slow interrupts into one penalty. Timing is Class 2, not a substitute for Class 1.
4. **Product VAD is part of the system.** Matching every API to the same `silence_duration_ms` is not "fairer"; it is a different product. Report the shipped default (or the knob you actually set) next to the score.
5. **Replay ≠ conversation.** Replay benches cannot test whether the model's own speech causes the next user event. Class 3 needs Interactive (FDB-v2), a segmenter (MTR), or humans. Those setups cost more and drift with examiner models.
6. **Synthetic overlap is clean.** TTS barge-in has sharp onsets and little bleed. Real dual-channel sets (TurnBench, HumDial, SID-Bench) have backchannels, echo, and mid-turn pauses that inflate interruption false positives.
7. **Judge metrics are optional and expensive.** FDB v1 interruption GPT scores and v1.5 behavior / prosody judges need extra model credentials. Timing-only runs are still valid; do not mix judged and unjudged leaderboards.
8. **ZH coverage is uneven.** Many papers list "multilingual" because one Chinese subset exists. Check which tasks are actually translated before claiming a Chinese result.
9. **Component ≠ system.** An EOT detector score is not a dialogue-product score. Keep Granularity visible. A Challenge number is comparable only under that frozen protocol.
10. **Adjacent ≠ Interaction.** VoiceBench / WildSpeech / VocalBench are speech understanding. A high number there does not mean the model can hold the floor. τ-Voice pass@1 is Task; its interrupt rate is Interaction.

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

See [CONTRIBUTING.md](CONTRIBUTING.md) ([中文](CONTRIBUTING.zh-CN.md)). Put each row in the **class that is actually scored**, not the venue or the repo. The same paper may appear in more than one class. Always update **both** `README.md` and `README.zh-CN.md`.
