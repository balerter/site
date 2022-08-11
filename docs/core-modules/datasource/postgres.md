The `datasource.postgres` module allows make queries to a **Postgres** datasource

Usage:

```lua title="script.lua"
local db = require('datasource.postgres.<NAME_FROM_CONFIG>')
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
local db = require('datasource.postgres.dev')

local res, err = db.query("SELECT id, name FROM users")
if err ~= nil then
    return
end

-- res
{
    {
        id = 1,
        name = 'root',
    },
    {
        id = 2,
        name = 'admin',
    },
    {
        id = 4,
        name = 'user1',
    },
}
```
