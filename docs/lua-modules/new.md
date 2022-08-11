A simple example

Method `add` with two arguments, returns sum

```
|
| modules
  | math.lua
``` 

```lua title="modules/math.lua"
local M = {}

local function add(a, b)
    return a + b
end

rawset(M, 'add', add)

return M
```

An example:

```lua title="script.lua"
local math = require('math')

local res = math.add(10, 20)

print(res) 

-- 30
```