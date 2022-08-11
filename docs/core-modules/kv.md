??? success "Core API"
    This module available in Core API

The `kv` _(key/value)_ module use for store Key/Value pairs

KV storage is global for all scripts

Usage:

```lua title="script.lua"
local kv = require('kv')
```

> All keys and values is strings. You can cast it in your scripts
> For example, if you saved a number, you will get a string!

## Methods

### all 

`all() data, error`

Get all KV pairs

```lua title="script.lua"
local data, err = kv.all()
if err ~= nil then
    print('an error occurred: ' .. err)
    return
end
```

### put 

`put(<NAME>, <VALUE>) error`

Save `VALUE` with key `NAME`

If the key already exists, an error will be returned

```lua title="script.lua"
local err = kv.put('key', 'value')
if err ~= nil then
    print('unable to put the variable in KV: ' .. err)
    return
end
```

### get 

`get(<NAME>) string, error`

Get a value by key `NAME`

If the key not exists, an error will be returned

```lua title="script.lua"
local value, err = kv.get('key')
if err ~= nil then
    print('a variable not exists in KV: ' .. err)
    return
end

print('value: ' .. value)
```

### upsert 

`upsert(<NAME>, <VALUE>) error`

Save or update a record by key `NAME` with value `VALUE`

If the key already exists, it will be rewrite with new value

```lua title="script.lua"
local err = kv.put('key', 'value')
kv.upsert('key', 'new value')
```

### delete 

`delete(<NAME>) error`

Delete a record with key `NAME`

If the key not exists, an error will be returned

```lua title="script.lua"
local value, err = kv.delete('key')
if err ~= nil then
    print('a variable not exists in KV: ' .. err)
    return
end

print('variable "key" has been deleted')
```
