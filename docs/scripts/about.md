For script use language: **Lua 5.1**

Official lua documentation [site](http://www.lua.org/manual/5.1/)

??? info "for developers"
    We use Golang library [https://github.com/yuin/gopher-lua](https://github.com/yuin/gopher-lua)

A simple example. Comments in lua scripts have prefix `--`

```lua title="script.lua"
-- in the head of script you can define some meta-tags. 
-- See more in section 'meta-tags'
-- @cron 0 * * * *

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

### Naming

Script name builds by next pattern:

`<provider type>.<provider name>.<name>`

Where:

- _provider type_ is string `file`, `folder` or `postgres` 
- _provider name_ is provider name from the config file

For `folder` and `file` providers file name will be take as script name.
If suffix `.lua` is present, it will be trimmed.



Example:

```yaml title="config.yaml"
scripts:
  folder:
    - name: scripts
      path: /opt/scripts
      mask: '*.lua'
  file:
    - name: demo1
      filename: /path/to/demo.lua
```

Script names:

```
folder.scripts.demo
```
