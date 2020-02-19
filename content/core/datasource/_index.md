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
- [Clickhouse](clickhouse)
- [Postgres](postgres)
- [Prometheus](prometheus)

### Null поля в источниках Clickhouse и Postgres

Если в результате запроса вернулось значение `null` для какого-либо поля, то обратите внимание, что при итерации по результатам запроса в Lua-скрипте с помощью `pairs`, это поле вы не получите. Поведение будет аналогично тому, как если обратиться к несуществующему полю. Будет возвращен `nil`

Пример:

Поле token может вернуть строку или null.
В этом случае, если в строке поле token было null, то эта строка даже не будет выведена. Это особенность реализации функции pairs.

```
res = pg.query('SELECT name, token FROM users')


for _, row in pairs(res) do
    for columnName, columnValue in pairs(row) do
        print(columnName .. ' = ' .. columnValue)
    end
end
```

Вы можете напрямую проверить содержимое поля `token` - в этом случае вы получите `nil`

```
res = pg.query('SELECT name, token FROM users')

for _, row in pairs(res) do
    print(row.name)
    print(row.token) -- row.token равняется nil
end
```
