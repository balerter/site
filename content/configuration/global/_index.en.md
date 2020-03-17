---
title: "Global"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 6
---

In the `global` section describes common settings

```
global:
  sendStartNotification:
    - slack-notification
  sendStopNotification:
    - slack-notification
  api:
    address: 127.0.0.1:2000
    metrics: true
```

### `sendStartNotification` 

Channels list, which will be send notification about application **start**. If omit, message will not be send.

### `sendStopNotification` 

Channels list, which will be send notification about application **stop**. If omit, message will not be send.

### `api`

HTTP API server settings

- `address` (by default `127.0.0.1:2000`) - listen address

- `metrics` (boolean, by default `false`) - if `True`, expose Prometheus metrics by `<API_ADDRESS>/metrics` address
  
### `storages`

Storage settings for core-modules.
You should set storage name, described in section [storages/core](../storages/core). Use a format:  
`<STORAGE_TYPE>.<STORAGE_NAME>`. Except for builtin storage - `memory` 

> By default for all modules uses builtin value - `memory`

- alert: storage for Alerts data  
- kv: storage for KV data

An example:
```
storages:
  core:
    file:
      - name: primary1
        path: /tmp/primary1.bin
...
global:
  storages:
    alert: file.primary1
    kv: file.primary1
```  