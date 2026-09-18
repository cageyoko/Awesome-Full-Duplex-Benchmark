# Interaction

**[Index](README.md) · [中文](interaction.zh-CN.md)**

This class scores **when to speak, when to stop, and when to stay silent**. It does not score whether the words are right (that is [Content](content.md) / [Task](task.md)), or how many milliseconds the action took (that is [Timing](timing.md)).

Do **not** average these subclasses into one TOR: pause wants fewer takeovers; turn-taking wants more.

Incoming sound while the model is talking:

```
Is it addressed to you?
  ├─ no / not speech          → Filter
  ├─ yes, but not claiming the floor  → Backchannel
  └─ yes, and claiming the floor      → Interrupt

Reject = a scoring bucket for “correctly not accepting”
          (often Filter + user Backchannel + false interrupts).
```

## Subclasses

| Subclass | What happened | Correct action | Typical miss |
|:--|:--|:--|:--|
| **Pause** | Mid-turn silence; the user is not done | Keep listening; do not barge in | Treat the gap as EOT |
| **Turn** | User finished; the floor is open | Take the turn | Stay silent, or take it too early |
| **Backchannel** | Short continuer (“mm”, “uh-huh”). Still addressed to you, not a floor claim | If *user* BCs while you talk: keep talking. If *you* should BC: short ack, not a full turn | Stop and answer “mm”; or launch a paragraph when only “mm” was needed |
| **Interrupt** | User wants the floor while you speak | Stop, then take the new intent | Keep reading the old sentence |
| **Filter** | Side talk, TV, noise — not to you | Ignore; hold state | Answer the noise |
| **Reject** | HumDial-style “this overlap is not a legal interrupt” | Do not take over | False accept. Overlaps Filter and user Backchannel; not a fourth user move |

Backchannel has two directions. FDB v1 ICC asks whether the *system* backchannels at TRPs. FDB v1.5 user-backchannel asks whether the *system* wrongly stops when the user only hummed.

## Where it shows up

FDB v1 (pause / turn / BC / interrupt), FDB v1.5 (interrupt / BC / filter), FD-Bench, HumDial (interrupt / reject), SID-Bench, TurnBench, Talking Turns, Easy-Turn (complete / incomplete / backchannel / wait), τ-Voice (responsiveness / interrupt rate / selectivity).

See [Metric notes](../README.md#metric-notes) for TOR direction and the FDB backchannel rule (`< 1 s` and `≤ 3` words).
