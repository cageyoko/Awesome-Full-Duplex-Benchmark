# Task

**[Index](README.md) · [中文](task.zh-CN.md)**

This class scores **getting work done while the user is talking** — tools, arguments, chained calls, under disfluency. Chat-only systems should mark the class **N/A**, not zero.

[Content](content.md) Instruction asks “are you still doing the requested thing?”. Task asks “did the API / database / policy step actually fire correctly?”. [Interaction](interaction.md) take-turn on a tool bench is a side signal, not the Task score.

## Subclasses

| Subclass | What it asks | Typical miss |
|:--|:--|:--|
| **Tool select** | Right function / API | Plausible but wrong tool |
| **Args** | Slots filled from speech | Drops a date, swaps a city after ASR noise |
| **Chain** | Multi-step calls stay consistent | Step 1 works, step 2 uses a stale id; Pass@1 dies |
| **Disfluency** | Still correct under filler, pause, hesitation, false start, self-correction | Treats a restart as a second intent; calls twice |

FDB v3 is the main open duplex tool bench with **real** disfluent speech (four domains). τ-Voice is the other first-class row: 278 τ²-bench customer-service tasks, a full-duplex user simulator, and pass@1 against the database. Its interrupt rate / selectivity sit in [Interaction](interaction.md); latency sits in [Timing](timing.md).

VoiceAgentBench / AudioCRAG are spoken tool-use but not full-duplex floor control — they live under Adjacent. Text τ-bench / BFCL stay off this list.
