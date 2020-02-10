---
title: "Раздел Scripts"
date: 2020-02-04T16:48:31+03:00
draft: false
---

В секции `scripts.sources` описываются источники скриптов. В данный момент поддерживается только тип `folder`

- [folder](folder)

```
scripts:
  sources:
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'
        update_interval: 5s
```

