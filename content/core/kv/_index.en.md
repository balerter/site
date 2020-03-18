---
title: "KV"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 2
---

The `kv` _(key/value)_ module use for store Key/Value pairs

KV storage is global for all scripts

Usage:

```
local kv = require('kv')
```

> All keys and values is strings. You can cast it in your scripts
> For example, if you saved a number, you will get a string!

### Methods

#### `put(<NAME>, <VALUE>) error`

Save `VALUE` with key `NAME`

If the key already exists, an error will be returned 

```
local err = kv.put('key', 'value')
if err ~= nil then
    print('unable to put the variable in KV: ' .. err)
    return
end
```

#### `get(<NAME>) string, error`

Get a value by key `NAME`

If the key not exists, an error will be returned 

```
local value, err = kv.get('key')
if err ~= nil then
    print('a variable not exists in KV: ' .. err)
    return
end

print('value: ' .. value)
```

#### `upsert(<NAME>, <VALUE>) error`

Save or update a record by key `NAME` with value `VALUE` 

If the key already exists, it will be rewrite with new value 

```
local err = kv.put('key', 'value')
kv.upsert('key', 'new value')
```

#### `delete(<NAME>) error`

Delete a record with key `NAME`

If the key not exists, an error will be returned 

```
local value, err = kv.delete('key')
if err ~= nil then
    print('a variable not exists in KV: ' .. err)
    return
end

print('variable "key" has been deleted')
```
