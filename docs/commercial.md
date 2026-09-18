# Commercial API evals

**[Index](../README.md) · [中文](commercial.zh-CN.md)**

What a vendor puts on the launch blog is **not** the same as a full-duplex report card. Most official numbers are speech understanding, audio reasoning, or tool calling. Floor control is usually internal, or only shows up when a third-party bench calls the API.

This page tracks **which sets they headline**. It is not a leaderboard. Scores move with model versions.

## Official vs third-party

| Kind | Who runs it | Typical sets | What it can claim |
|:--|:--|:--|:--|
| **Official headline** | The vendor | Big Bench Audio, VoiceBench, ComplexFuncBench Audio, internal MOS | They chose the protocol. Often not Interaction TOR |
| **Third-party duplex** | FDB / τ-Voice / [Artificial Analysis](https://artificialanalysis.ai/speech-to-speech) | FDB (AA uses a subset), τ-Voice | Comparable floor + tool numbers, if the API was actually called |
| **Third-party adjacent** | Scale, VoiceBench authors, Coval, AA | Audio MultiChallenge, VoiceBench, WildSpeech, Big Bench Audio | Content / reasoning / latency. Do not mix with [Interaction](interaction.md) |

A “dataset” is the wrong word for several of these. FDB v2, τ-Voice, OpenAI’s RUN harness, and Seed’s human tests are **protocols** (simulator, examiner, or live calls), not a frozen wav pack.

## What each vendor headlines

### GPT Realtime (OpenAI)

| They report | Class here | Notes | Source |
|:--|:--|:--|:--|
| **Big Bench Audio** | Adjacent (audio reasoning) | Headline number on the launch post. Not pause / interrupt | [gpt-realtime](https://openai.com/index/introducing-gpt-realtime/) |
| Internal alphanumeric (phone / VIN, multilingual) | Content / Speech | No public split | same |
| Cookbook **CRAWL / WALK / RUN** | Timing / Interaction / Task | Their recommended product eval. RUN is a simulated full-duplex caller; docs say it takes inspiration from τ-Voice. Not a released shared set | [Realtime eval guide](https://developers.openai.com/cookbook/examples/audio/voice_agent_evaluation) |

Third parties also run Realtime on [FDB v2](../README.md#3-multi-turn-content), [FDB v3](../README.md#4-task-and-tools), [τ-Voice](../README.md#4-task-and-tools), [Audio MultiChallenge](../README.md#3-multi-turn-content), and the [AA Speech-to-Speech Index](#artificial-analysis-speech-to-speech-index).

### Gemini Live / Native Audio (Google)

| They report | Class here | Notes | Source |
|:--|:--|:--|:--|
| **ComplexFuncBench Audio** | Task (closed) | 71.5% on the Dec 2025 native-audio post. Public [ComplexFuncBench](https://github.com/zai-org/ComplexFuncBench) is text; the audio variant is not rerunnable here | [Gemini audio update](https://blog.google/products-and-platforms/products/gemini/gemini-audio-model-updates/) |
| Internal instruction adherence | Content | 90% on that post; no public items | same |
| Unnamed multi-turn context | Content | Blog claim only | same |

Third parties also run Live / Gemini audio on FDB v3, τ-Voice, Audio MultiChallenge, and VoiceBench. Gemini 3 Pro Thinking is the Audio MultiChallenge high-water mark in the paper (54.65% pass).

### Grok Voice (xAI)

| They report | Class here | Notes | Source |
|:--|:--|:--|:--|
| **Big Bench Audio** | Adjacent (audio reasoning) | Launch claim; AA also reports it as the reasoning leg of the S2S index | [Grok Voice Agent API](https://x.ai/news/grok-voice-agent-api) |
| Time-to-first-audio | Timing | Sub-second product claim | same |
| Blind human vs OpenAI Realtime | Speech | Pronunciation / accent / prosody, not TOR | same |

Third parties also run Grok Voice on FDB v3, τ-Voice, and the AA S2S index. Not in the Audio MultiChallenge paper table.

### Seeduplex / SeedDuplex (ByteDance Seed)

| They report | Class here | Notes | Source |
|:--|:--|:--|:--|
| Endpoint MOS, dialogue-fluency MOS | Interaction / Timing | +8% / +12% vs the previous Doubao half-duplex stack | [Seeduplex](https://research.doubao.com/zh/seeduplex) |
| Barge-in rate, interrupt latency, false-response / false-interrupt | Interaction / Timing | Relative deltas vs their own half-duplex; complex acoustic scenes | same |
| Live human–human baseline | Interaction | Product MOS, not a public scorer | same |
| “Mainstream app voice call” bake-off | — | Unnamed competitors | same |

No public FDB / τ-Voice / VoiceBench row from the vendor. Treat these as **internal product metrics**.

### Qwen-Omni (Alibaba)

| They report | Class here | Notes | Source |
|:--|:--|:--|:--|
| **VoiceBench** | Adjacent | Official voice-chat headline (Qwen3-Omni-Thinking 89.5 in the tech report) | [Qwen3-Omni](https://github.com/QwenLM/Qwen3-Omni) / [arXiv 2509.17765](https://arxiv.org/abs/2509.17765) |
| MMAU / MMSU | Adjacent (audio reasoning) | Not dialogue floor control | same |
| ASR / S2TT / music sets | — | Understanding, not duplex | same |
| First-packet latency (234 ms) | Timing | System measurement, not FDB | same |

The tech report does **not** headline FDB or τ-Voice. Audio MultiChallenge does include Qwen3-Omni (audio out, 24.34% pass). AA’s S2S board now also lists Qwen realtime SKUs on Big Bench Audio / FDB / τ-Voice.

## Artificial Analysis Speech-to-Speech Index

This is the main **independent commercial scoreboard**, not a new protocol. [Announcement](https://artificialanalysis.ai/articles/announcing-the-artificial-analysis-speech-to-speech-index) / [live board](https://artificialanalysis.ai/speech-to-speech). Datasets they host or clean sit under [huggingface.co/datasets/ArtificialAnalysis](https://huggingface.co/datasets/ArtificialAnalysis).

Equal weight, three legs (plus they publish TTFA / cost on the side):

| AA leg | Maps to here | Public artifact | Not |
|:--|:--|:--|:--|
| **Speech Reasoning** | Adjacent (audio reasoning) | [Big Bench Audio](https://huggingface.co/datasets/ArtificialAnalysis/big_bench_audio) — 1,000 EN TTS items from BBH (Formal Fallacies, Navigate, Object Counting, Web of Lies) | Instruction after you already spoke |
| **Conversational Dynamics** | Interaction | Full-Duplex-Bench **subset** (pause / turn / interrupt / backchannel) | Their composite ≠ official FDB paper tables |
| **Agentic Performance** | Task | τ-Voice (airline / retail / telecom) | Cookbook RUN |

Do **not** treat the single AA % as Interaction TOR. It averages three classes.

Also on that HF org, and **not** S2S dialogue:

| HF repo | AA product | Class here |
|:--|:--|:--|
| `VoxPopuli-Cleaned-AA`, `Earnings22-Cleaned-AA` | [AA-WER](https://artificialanalysis.ai/articles/aa-wer-v2) STT (with held-out **AA-AgentTalk**, not public) | [Speech](speech.md) transcription, not duplex model speech |
| `AA-LCR`, `AA-Omniscience-Public`, `AA-Briefcase-Lite`, `ITBench-AA` | Text Intelligence Index | Stay off this list |

## Third-party coverage (who was actually called)

Empty cell = not in that paper’s table, not “the API cannot run it”.

| Bench | GPT Realtime | Gemini Live | Grok Voice | Seeduplex | Qwen-Omni |
|:--|:--:|:--:|:--:|:--:|:--:|
| **FDB v2** | ✓ | | | | |
| **FDB v3** | ✓ | ✓ | ✓ | | |
| **τ-Voice** | ✓ | ✓ | ✓ | | |
| **Audio MultiChallenge** | ✓ | ✓ | | | ✓ |
| **VoiceBench** | GPT-4o-Audio* | ✓ | | | ✓ (official) |
| **Coval S2S** | ✓ | ✓ | | | |
| **AA S2S Index** | ✓ | ✓ | ✓ | | ✓* |

\* VoiceBench tables usually list GPT-4o-Audio, not always the later Realtime SKU. AA’s later S2S board lists Qwen realtime SKUs; Seeduplex still does not appear there.

If you only need one public stack that hits GPT, Gemini, and Grok on **floor + tools**, use FDB v3 and τ-Voice — or read the AA index and then **split the three legs**. Add Audio MultiChallenge for multi-turn content. Do not fill Seed gaps by averaging VoiceBench or MOS into Interaction.

## Do not mix

1. Big Bench Audio / VoiceBench / MMAU / the AA composite ≠ [Interaction](interaction.md) TOR.
2. ComplexFuncBench Audio ≠ FDB v3 / τ-Voice. Same class family (Task), different protocol, and the audio set is closed.
3. Seed MOS deltas are vs Doubao half-duplex, not vs GPT.
4. OpenAI RUN and τ-Voice are cousins, not the same harness. A cookbook score is not a τ-Voice pass@1.
5. When a blog says “industry-leading” without a named public protocol, leave it off the coverage map.

See [Adjacent](../README.md#adjacent-spoken-understanding-and-half-duplex-agents) for the half-duplex rows, and the five class notes for what a number is allowed to mean.
