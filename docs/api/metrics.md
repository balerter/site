The Balerter expose prometheus metrics on `serviceAddress` if it's defined in the configuration. (see [configuration](../configuration/api))

Under hood, we use [prometheus default library](https://github.com/prometheus/client_golang) for expose metrics. 
This library expose some default application metrics:

- go_gc_duration_seconds
- go_goroutines 
- go_info
- go_memstats_alloc_bytes 
- go_memstats_frees_total 
- go_memstats_gc_cpu_fraction
- go_memstats_heap_alloc_bytes
- go_threads 

...and more

The Balerter add 3 custom metrics, which has the prefix `balerter_`

- `balerter_info_version`
- `balerter_scripts_active`
- `balerter_alert_status`

## `balerter_info_version`

This metric contains the balerter version as metrics label. The metrics value is always equals to 1.

An example:

```
balerter_info_version{version="v0.10.0"} 1
```

## `balerter_scripts_active`

This metric contains the script name as metric label `name`. The metrics value equals to 1 if the script is active, and 0 if the script is inactive.

An example:

```
balerter_scripts_active{name="folder.dbg.d1"} 1
balerter_scripts_active{name="folder.dbg.d2"} 1
balerter_scripts_active{name="folder.f2.foo"} 1
```

## `balerter_alert_status` 

This metric contains the current alert statuses. An alert name (id) presents as label `name`. The metric value present the alert level

- Success - 1
- Warning - 2
- Error - 3

An example:

```
balerter_alert_status{name="foo"} 3
balerter_alert_status{name="bar"} 1
balerter_alert_status{name="baz"} 2
```
