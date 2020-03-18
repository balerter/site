---
title: "Раздел storages"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 5
---


In section `storages` describes:
- core : for store Alert data and KV data 
- upload : for upload files (usually images)

```
storages:
  core:
    file:
      - name: primaryFile
        path: /path/to/file
        timeout: 1s
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

