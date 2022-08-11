The `datasource.clickhouse` module allows make queries to a Clickhouse cluster

Usage:

```lua title="script.lua"
local db = require('datasource.clickhouse.<NAME_FROM_CONFIG>')
```

## Methods

### query 

`query('<SQL QUERY>') result, error`

Send a query. If an error occurred, it will be returned as second value

A result format:

```
{
    -- row 1
    {
        <FIELD1_NAME> = <FIELD1_VALUE>,
        <FIELD2_NAME> = <FIELD2_VALUE>,
        ...
    },
    -- row 2
    {
        <FIELD1_NAME> = <FIELD1_VALUE>,
        <FIELD2_NAME> = <FIELD2_VALUE>,
        ...
    },
    -- row N
    ...
}
``` 

An example:

```lua title="script.lua"
local db = require('datasource.clickhouse.dev')

local res, err = db.query("SELECT table, sum(bytes) AS size FROM system.parts WHERE active AND database = 'system' GROUP BY table")
if err ~= nil then
    return
end

-- res 
{
    {
        table = 'query_thread_log',
        size = 943846427
    },
    {
        table = 'metric_log',
        size = 656645852
    },
    {
        table = 'query_log',
        size = 997251520
    },
    {
        table = 'part_log',
        size = 2037035728
    }
}
```
