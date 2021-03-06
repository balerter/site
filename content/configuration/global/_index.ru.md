---
title: "Раздел global"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 6
---

В секции `global` описываются общие настройки приложения

```
global:
  luaModulesPath: /modules/?.lua;/modules/?/?.lua
  sendStartNotification:
    - slack-notification
  sendStopNotification:
    - slack-notification
  api:
    address: 127.0.0.1:2000
    metrics: true
  storages:
    alert: file.primaryFile
    kv: memory
```

### `luaModulesPath`

> По умолчанию: "./?.lua;./modules/?.lua;./modules/?/init.lua" 

Путь с папке с lua модулями

### `sendStartNotification` 

Список каналов, куда будет отправлено уведомление **о старте** приложения. Если не указано, уведомление отправлено не будет.

### `sendStopNotification` 

Список каналов, куда будет отправлено уведомление **об остановке** приложения. Если не указано, уведомление отправлено не будет.

### `api`

Настройки HTTP API сервера приложения

- `address` (по умолчанию `127.0.0.1:2000`) - адрес, на котором будет слушать HTTP API сервер

- `metrics` (boolean, по умолчанию `false`) - если `True`, то по адресу `<API_ADDRESS>/metrics` будут доступны Prometheus метрики

### `storages`

Какое хранилище использовать для соответствующего core-модуля. Тут следует указыать имя хранилища из секции файла конфигурации [storages/core](../storages/core) в следующем формате:
`<STORAGE_TYPE>.<STORAGE_NAME>`. Исключение для встроенного значения `memory` 

> По-умолчанию для всех модулей используется значение `memory`, которое указывает, что данных хранятся только в памяти

- alert: для хранения данных об алертах  
- kv: для хранения данных KV

Пример:
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