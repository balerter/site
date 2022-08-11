The module `datasource.loki` allows get data from sources, which support query language LogQL by **Grafana Loki**

See more about [Loki](https://github.com/grafana/loki)

```lua title="script.lua"
local loki = require('datasource.loki.<NAME_FROM_CONFIG>')
```

## Methods

### query

`query('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

[Instant Query](https://github.com/grafana/loki/blob/master/docs/api.md#get-lokiapiv1query)

A result format:

```
{
    {
        lables = {
            <LABEL_NAME> = <LABEL_VALUE>,
            ...
        },
        entries = {
            {
                timestamp = <TIMESTAMP>,
                line = <VALUE>
            },
            ...
        }
    },
    ...
}
``` 

The options:

```
{
    time = <TIME RFC3339|Timestamp> -- Evaluation timestamp
    direction = [backward|forward]  -- Determines the sort order of logs. Supported values are forward or backward. Defaults to backward
    limit = <NUMBER>                -- The max number of entries to return
}
```

For example:

```lua title="script.lua"
local loki = require('datasource.loki.dev')

local res, err = loki.query('{service="srv1"}')
if err ~= nil then
    return
end

-- results:
{
    ...
    {
        labels = {
            service = srv1
            level = 1
        }
        entries = {
            {
                timestamp = 1581934085
                line = 'Log line'
            }
        }
    },
    {
        labels = {
            service = srv1
            level = 2
        }
        entries = {
            {
                timestamp = 1581934085
                line = 'Log line'
            }
        }
    },
    ...
 }
```

### range 

`range('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

[Range Query](https://github.com/grafana/loki/blob/master/docs/api.md#get-lokiapiv1query_range)

Result format same as `query` result

The options:

```
{
    start = <TIME RFC3339|Timestamp>    -- start time
    end = <TIME RFC3339|Timestamp>      -- end time
    step = <NUMBER>                     -- Query resolution step width in duration format or float number of seconds
    direction = [backward|forward]      -- Determines the sort order of logs. Supported values are forward or backward. Defaults to backward
    limit = <NUMBER>                    -- The max number of entries to return
}
```

