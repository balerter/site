---
title: "Preset modules"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 3
---

## Preset modules

By default Balerter distributed with some preset modules, which placed in the `modules` folder.

They are not needed for the balerter functional

### h (helper)

Usage:

```
local h = require('h')
```

#### Methods

#### `tableToMap(table, keyFieldName) table, error`

Convert lua table to hash-table with keys as 'keyFieldName' value  

An example:

```
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

#### `print(table)`

Beautify print table or any value to the console

```
local t = { ['foo'] = { ['bar'] = 42 } }

h.print(t)

-- a result
{
    foo = {
        bar = 42
    }
}
```

### json

> https://github.com/rxi/json.lua

Allows encode/decode json

```
json = require('json')

json.encode({ 1, 2, 3, { x = 10 } }) -- Returns '[1,2,3,{"x":10}]'
json.decode('[1,2,3,{"x":10}]') -- Returns { 1, 2, 3, { x = 10 } }
```