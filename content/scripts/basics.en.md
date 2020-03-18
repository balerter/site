---
title: "Basics"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 1
---

For script use language: **Lua 5.1** 

Official lua documentation [site](http://www.lua.org/manual/5.1/) 

> For developers: we use Golang library https://github.com/yuin/gopher-lua 

A simple example. Comments in lua scripts have prefix `--` 

```
-- in the head of script you can defined some meta-tags. See more in section 'meta-tags'
-- @interval 5m

-- store 1e9 to the variable sizeLimit  
local sizeLimit = 1000000000

-- add Log module
local log = require("log")
-- add Clickhouse datasource
local ch1 = require("datasource.clickhouse.ch1")

-- send query to the clickhouse datasource
local res, err = ch1.query("SELECT sum(bytes) AS size FROM system.parts WHERE active")
-- if an error occurred, print the error and exit
if err ~= nil then
    log.error("clickhouse 'ch1' query error: " .. err)
    return
end

-- get first item (first array element in Lua is 1, not 0!)
-- and get field size
local currentSize = res[1].size

if currentSize > sizeLimit then
    alert.error("clickhouse-disk-space", "Check disk space in Clickhouse cluster! Current busy: " .. tostring(currentSize))
else
    alert.success("clickhouse-disk-space", "Clickhouse disk space - ok")
end 
```