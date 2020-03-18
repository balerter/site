---
title: "Create a lua module"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 2
---

A simple example

Method `add` with two arguments, returns sum

```
|
| modules
  | math.lua
``` 

```
-- math.lua

local M = {}

local function add(a, b)
    return a + b
end

rawset(M, 'add', add)

return M
```

An example:

```
local math = require('math')

local res = math.add(10, 20)

print(res) 

-- 30
```