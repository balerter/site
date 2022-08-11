??? success "Core API"
    This module available in Core API

- [clickhouse](clickhouse.md)
- [prometheus](prometheus.md)
- [postgres](postgres.md)
- [mysql](mysql.md)
- [loki](loki.md)

A `datasource` module allows get data from different sources

Usage:

```lua title="script.lua"
local ds1 = require('datasource.<TYPE>.<NAME>)
```

- type - datasource type
    - clickhouse
    - prometheus
    - postgres
    - etc...
- name - datasource name from configuration

Examples:

```yaml title="config.yaml"
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

Usage modules in a script:
```lua
local chDev = require('datasource.clickhouse.dev')
local chProd = require('datasource.clickhouse.prod')
local pgDev = require('datasource.postgres.dev')
local pgProd = require('datasource.postgres.prod')
local prom1 = require('datasource.prometheus.prom1')
```

## Null fields (Clickhouse, Postgres, MySQL)

If your query returns a data with null values, you not may get these fields by iteration loop.

The behavior is the same as 'nil' value in the Lua table

An example:

The 'token' field may return a string or null.
In this example, if returns null, this string will not be printed

```lua title="script.lua"
res = pg.query('SELECT name, token FROM users')


for _, row in pairs(res) do
    for columnName, columnValue in pairs(row) do
        print(columnName .. ' = ' .. columnValue)
    end
end
```

You can straight check value to nil

```lua title="script.lua"
res = pg.query('SELECT name, token FROM users')

for _, row in pairs(res) do
    print(row.name)
    print(row.token) -- row.token equals to nil
end
```
