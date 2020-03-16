---
title: "Раздел storages"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 5
---

В секции `storages` описываются хранилища:
- core : для хранения данных KV и Алертов 
- upload : для загрузки файлов. Обычно это используется для загрузки изображений (графиков)

```
storages:
  core:
    file:
      - name: primaryFile
        path: /path/to/file
  upload:
    s3:
      - name: dev
        region: us-east1
        key: SOME_KEY
        secret: SOME_SECRET
        endpoint: SOME_ENDPOINT
        bucket: SOME_BUCKET
```

## Core

- [file](core/file)

## Upload

- [s3](upload/s3)

