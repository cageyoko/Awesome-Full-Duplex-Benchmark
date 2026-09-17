# Contributing

This list is for **evaluation**. A new model with a two-page "we also report TOR" section belongs on [Awesome-Full-Duplex-SDM](https://github.com/Ruiqi-Yan/Awesome-Full-Duplex-SDM), not here — unless it introduces a reusable protocol, dataset, or metric definition.

## Add or fix an entry

1. Open a PR against `README.md`.
2. Put the row in the section that matches **what is scored**, not the paper title.
3. Fill every legend column. Use `—` or `?` instead of inventing a value.
4. Link arXiv / venue, code, data, and demo when they exist. Do not link a GitHub that is only a paper PDF.
5. In **Headline metrics**, write the short names and the direction (↑/↓) if it is not obvious. If TOR flips by task, say so.
6. If you have run the bench, a one-line caveat in [Metric notes](README.md#metric-notes) is more useful than another adjective in the title.

## Suggested PR title

`Add <BenchName> (<year>)` or `Fix <BenchName> protocol / links`.

## What we will not merge

- Duplicate of an existing row (update the old one).
- Training-only datasets with no eval split or scoring script.
- Closed product blog posts that do not define a protocol someone else can rerun or cite.
- Marketing leaderboards with no metric definition.

## Local preview

This repo is a single Markdown file. GitHub rendering is the preview.
