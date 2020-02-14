---
title: "Создание lua модуля"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 2
---

Пример простого модуля, который эспортирует метод `add`. 

`add` принимает два аргумента, складывает их и возвращает результат

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

Пример использования:

```
local math = require('math')

local res = math.add(10, 20)

print(res) 

-- 30
```