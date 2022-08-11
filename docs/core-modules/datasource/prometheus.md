The `datasource.prometheus` module allows send queries to a **Prometheus** datasource

It may be any source, which supports a PromQL.
For example [Victoria Metrics](https://victoriametrics.com)

Usage:

```lua title="script.lua"
local db = require('datasource.prometheus.<NAME_FROM_CONFIG>')
```

## Methods

### query 

`query('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

[Instant Query](https://prometheus.io/docs/prometheus/latest/querying/api/#instant-queries)

A result format:

```
{
    {
        metrics = {
            <METRIC_NAME> = <METRIC_VALUE>,
            ...
        },
        value = {
            timestamp = <TIMESTAMP>,
            value = <VALUE>
        }
    },
    ...
}
``` 

An options:

```
{
    time = <TIME RFC3339|Timestamp> -- Evaluation timestamp
}
```

An example:

```lua title="script.lua"
local prom = require('datasource.prometheus.dev')

local res, err = prom.query("node_cpu_seconds_total")
if err ~= nil then
    return
end

-- res 
{
    ...
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 7
            datacenter = dc1
            job = node_exporter
            mode = softirq
        }
        value = {
            timestamp = 1581934085
            value = 118687.2
        }
    },
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 6
            datacenter = dc1
            job = node_exporter
            mode = idle
        }
        value = {
            timestamp = 1581934085
            value = 3.95205464e+06
    },
    ...
 }
```

### range 

`range('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

[Range Query](https://prometheus.io/docs/prometheus/latest/querying/api/#range-queries)

A result format:

```
{
    {
        metrics = {
            <METRIC_NAME> = <METRIC_VALUE>,
            ...
        },
        values = {
            {
                timestamp = <TIMESTAMP>,
                value = <VALUE>
            },
            ...
        }
    },
    ...
}
``` 

An options:

```
{
    start = <TIME RFC3339|Timestamp>    -- start time
    end = <TIME RFC3339|Timestamp>      -- end time
    step = <NUMBER>                     -- Query resolution step width in duration format or float number of seconds
}
```

An example:

```lua title="script.lua"
local prom = require('datasource.prometheus.dev')

local res, err = prom.range("node_cpu_seconds_total")
if err ~= nil then
    return
end

-- res 
{
    ...
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 7
            datacenter = dc1
            job = node_exporter
            mode = softirq
        }
        values = {
            {
                timestamp = 1581837350,
                value = 186776.71
            },
            {
                timestamp = 1581840950,
                value = 186770.40
            },
            ...
        }
    },
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 6
            datacenter = dc1
            job = node_exporter
            mode = idle
        }
        values = {
            {
                timestamp = 1581837350,
                value = 186776.71
            },
            {
                timestamp = 1581840950,
                value = 186770.40
            },
            ...
        }
    },
    ...
 }
```