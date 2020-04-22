---
title: "Scripts"
date: 2020-02-04T16:48:31+03:00
draft: false
weight: 2
---

In the `scripts.sources` section describes script sources.

- [folder](folder)
- [file](file)

```
scripts:
  updateInterval: 5s
  sources:
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'
    file:
      - name: demo1
        filename: /path/to/demo.lua
```

### `updateInterval: <TIME INTERVAL>`

> By default: 1 minute

An interval for check changes in scrip sources

Possible suffixes: "ns", "us" (or "µs"), "ms", "s", "m", "h".
