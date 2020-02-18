---
title: "Раздел storages"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 5
---

В секции `storages` описываются настроки для подключения к хранилищам, куда можно загрузить файлы. Обычно это используется для загрузки изображений (графиков)

Поддерживаемые типы хранилища:
- [s3](s3)

```
storages:
  s3:
    - name: dev
      region: us-east1
      key: SOME_KEY
      secret: SOME_SECRET
      endpoint: SOME_ENDPOINT
      bucket: SOME_BUCKET
```
