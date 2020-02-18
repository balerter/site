---
title: "Datasource"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 6
---

Модуль `datasource` обеспечивает доступ к источникам данных. 

Формат подключения:

```
local ds1 = require('datasource.<TYPE>.<NAME>)
```

где
- type - это тип источника данных
    - clickhouse
    - prometheus
    - postgres
- name - это имя источника данных, определенное в файле конфигурации


Примеры:

Часть файла конфигурации
```
datasources:
  clickhouse:
    - name: dev
      ...
    - name: prod
      ...
  postgres:
    - name: dev
      ...
    - name: prod
      ...
  prometheus:
    - name: prom1
```

Подключение модулей в скрипте
```
local chDev = require('datasource.clickhouse.dev')
local chProd = require('datasource.clickhouse.prod')
local pgDev = require('datasource.postgres.dev')
local pgProd = require('datasource.postgres.prod')
local prom1 = require('datasource.prometheus.prom1')
```

Использование каждого типа источника данных смотрите далее
- [Clickhous](clickhouse)
- [Postgres](postgres)
- [Prometheus](prometheus)