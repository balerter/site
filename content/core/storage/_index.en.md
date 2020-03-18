---
title: "Storage"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 4
---

The `storage` module allows upload data to remote storage, described in configuration

Usage:

```
local storage = require('storage.<TYPE>.<NAME>')
```

- type - storage type
    - s3
- name - storage name from configuration


An example:

A configuration file
```
storages:
  s3:
    - name: dev
      ...
```

A script
```
local s3 = require('storage.s3.dev')
```

See more
- [s3](s3)