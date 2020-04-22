---
title: "Раздел Scripts"
date: 2020-02-04T16:48:31+03:00
draft: false
weight: 2
---

В секции `scripts.sources` описываются источники скриптов. В данный момент поддерживается только тип `folder`

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

> По-умолчанию: 1 минута

Интервал, с которым система будет проверять изменения в источниках скриптов и применять изменения, если они были

Допустимые суффксы для указания интервала: "ns", "us" (or "µs"), "ms", "s", "m", "h".
