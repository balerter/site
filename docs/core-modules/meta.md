??? failure "Core API"
    This module is not available in Core API

You can use this module for getting the information about the current script 

## Usage:

```lua title="script.lua"
local meta = require('meta')
```

## Methods

### priorExecutionTime 

`priorExecutionTime() float`

Returns prior execution time in seconds. 0 for the first execution

### cronLocation 

`cronLocation() string`

Returns cron location

If cron location not specified in the configuration, `Local` will be returned 

An example:

```lua title="script.lua"
local meta = require('meta')
local h = require('h')


h.print(meta.priorExecutionTime())
h.print(meta.cronLocation())
```

```
0.000154
UTC
```
