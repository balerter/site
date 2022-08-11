??? failure "Core API"
    This module is not available in Core API

The `file` module use for save/load local files

Usage:

```lua title="script.lua"
local file = require('file')
```

## Methods

### save 

`save(filename, body) error`

Save a file to the disk

```lua title="script.lua"
local err = file.save('example.txt', 'Hello World!')
if err ~= nil then
    print('an error occurred: ' .. err)
    return
end
```

### load 

`load(filename) body, error`

Load a file from the dist

```lua title="script.lua"
local body, err = file.load('example.txt')
if err ~= nil then
    print('unable to put the variable in KV: ' .. err)
    return
end

print(body)
```
