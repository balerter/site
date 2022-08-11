By default, Balerter distributed with some preset modules, 
which placed in the `modules` folder.

They are not needed for the balerter functional

## h (helper)

Usage:

```lua title="script.lua"
local h = require('h')
```

### tableToMap 

`tableToMap(table, keyFieldName) table, error`

Convert lua table to hash-table with keys as 'keyFieldName' value

An example:

```lua title="script.lua"
table = { 
    { date = '2020-01-01', id = 'a', name = 'aa'}, 
    { date = '2020-01-01', id = 'b', name = 'bb' },
    ... 
}

res, err = h.tableToMap(table, 'id')

-- res  
{
    'a' = { date = '2020-01-01', id = 'a', name = 'aa'}, 
    'b' = { date = '2020-01-01', id = 'b', name = 'bb' },
    ...
}
```

### print 

`print(table)`

Beautify print table or any value to the console

```lua title="script.lua"
local t = { ['foo'] = { ['bar'] = 42 } }

h.print(t)

-- a result
{
    foo = {
        bar = 42
    }
}
```

## json

> [https://github.com/rxi/json.lua](https://github.com/rxi/json.lua)

Allows encode/decode json

```lua title="script.lua"
json = require('json')

json.encode({ 1, 2, 3, { x = 10 } }) -- Returns '[1,2,3,{"x":10}]'
json.decode('[1,2,3,{"x":10}]') -- Returns { 1, 2, 3, { x = 10 } }
```

## csv

> [https://github.com/FourierTransformer/ftcsv](https://github.com/FourierTransformer/ftcsv)

Work with csv

An example:

```lua title="script.lua"
local db = require('datasource.postgres.pg1')
local log = require('log')
local csv = require('csv')
local h = require('h')

res, err = db.query('SELECT * FROM users')
if err ~= nil then
    log.error('query error: ' .. err)
    return
end

h.print(csv.encode(res, ","))
```