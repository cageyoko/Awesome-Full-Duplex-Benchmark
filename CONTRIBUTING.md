# Contributing

This list is for **evaluation**. A new model with a two-page "we also report TOR" section belongs on [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM), not here — unless it introduces a reusable protocol, dataset, or metric definition.

Sections follow **what is scored**, not the repo or the venue:

1. Interaction control
2. Timing
3. Multi-turn content
4. Task and tools
5. Speech and robustness

`Component` and `Challenge` are tags (Granularity / Protocol), not sections. The same paper may appear in more than one class.

## Add or fix an entry

1. Open a PR that updates **both** `README.md` (English) and `README.zh-CN.md` (Chinese). The two files must stay in sync. If you change a Class or subclass definition, update the matching notes under `docs/` (`*.md` and `*.zh-CN.md`).
2. Put the row in the class that matches **what is scored**. Duplicate the row if it is first-class in a second class (for example FDB v1 under Interaction and Timing).
3. Fill Class / Subclass, Granularity, Protocol, Stimulus (`Synthetic` / `Real` / `Mixed` / `Text`), Open (`Code + data` / `Code + weights` / `Code` / `Data` / `—`). Use `—` or `?` instead of inventing a value. Keep these tags in English in both files. Do not write `ZH / EN` unless both languages have a released eval split.
4. Link arXiv / venue, code, data, and demo when they exist. Do not link a GitHub that is only a paper PDF.
5. In **Headline metrics**, write the short names and the direction (↑/↓) if it is not obvious. If TOR flips by subclass, say so.
6. If you have run the bench, a one-line caveat in [Metric notes](README.md#metric-notes) / [指标注意事项](README.zh-CN.md#指标注意事项) is more useful than another adjective in the title.
7. Update the coverage map in both READMEs when the main claim changes.

## Suggested PR title

`Add <BenchName> (<year>)` or `Fix <BenchName> class / links`.

## What we will not merge

- Duplicate of an existing row in the **same** class (update the old one).
- A new Component or Challenge chapter.
- Training-only datasets with no eval split or scoring script.
- Closed product blog posts that do not define a protocol someone else can rerun or cite.
- Marketing leaderboards with no metric definition.
- A single scalar that averages Interaction subclasses.

## Local preview

GitHub rendering of `README.md` / `README.zh-CN.md` is the preview.
