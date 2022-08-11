??? failure "Core API"
    This module is not available in Core API

You can use this module for getting the information about request, if the script run with API call. 

## Usage:

```lua title="script.lua"
local api = require('api')
```

## Methods

### is_api

Returns `true`, if the script was run with API call

```lua title="script.lua"
local api = require('api')
isApi = api.is_api()
```

### query

Returns query arguments

An example:

Query: `...?name=foo&name=bar&baz=42`

```lua title="script.lua"
local api = require('api')
local h = require('h')

local q = api.query()
h.print(q)
```

``` title="result"
{
    name = {
        "foo"
        "bar"
    }
    baz = {
        "42"
    }
}
```

### url

Returns the request URL

### body

Returns the request Body

### method

Returns the request method

