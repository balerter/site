+++
title = "Lua Modules"
date = 2020-02-04T16:08:54+03:00
weight = 4
pre = "<b>IV. </b>"
+++

You can use external lua modules, wrote with the Lua language

You should place it to the `modules` folder

A module can be wrote in the single file. In this case module name will be same as filename

An example:

```
root
|
| modules
  | conv.lua
```
```
local conv = require('conv')
```

The module can be placed in one folder with several files. In this case folder must have file init.lua with export code 

An example:

```
root
|
| modules
  | conv.lua
  | money
    | convert.lua
    | compress.lua
    | init.lua
```
```
local money = require('money')
```

