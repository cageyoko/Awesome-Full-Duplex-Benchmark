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

FDB v3 is the main open duplex tool bench (real disfluent speech, four domains). τ-Voice (grounded customer-service tools + duplex user sim) is the other first-class paper in this class and is not yet a row in the main list.

VoiceAgentBench / AudioCRAG are spoken tool-use but not full-duplex floor control. Text τ-bench / BFCL stay off this list.
