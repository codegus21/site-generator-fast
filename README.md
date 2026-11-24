# site-generator-fast

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/codegus21/site-generator-fast/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/codegus21/site-generator-fast/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

Write a faster drop-in for make.fun's own makefun-site 1.0.0 that answers exactly as it does on every case; places go by CPU time, least first, and beating makefun-site, the house baseline, at 95% confidence only qualifies an entry for a place.

`solve.js` is a dependency-free ES module whose `run(input)` returns makefun-site 1.0.0's answer for every input `{ site, templates, files }`. It is an independent implementation of makefun-site's own rules (front matter, template dialect, Markdown subset, slug rule, report), written for speed: the Markdown renderer scans the body's lines once and writes output directly (no token objects), its inline renderer copies each plain run with one slice instead of escaping character by character, slugs are cached per build and take an ASCII fast path, templates are parsed once per build and rendered by a tree walker over a single flat scope object (a for-loop saves and restores the names it binds, which is exactly the reference's scope chain), and a source's card is built once and shared between its page and the lists that show it. On the kit's practice set it runs about 3.7x faster than the reference (CPU time), and its answers are byte-identical to the oracle's on all three practice cases.

## Run it

```sh
node main.ts
```

`main.ts` reads every case from `/input/cases.json`, answers each one alone with `run()` from `solve.js`, and writes `/output/answers.json`. Outside a container, `MAKEFUN_INPUT_DIR` and `MAKEFUN_OUTPUT_DIR` stand in for `/input` and `/output`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=jg0j15t7&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
