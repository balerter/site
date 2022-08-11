![biglogo](biglogo.png)

Balerter is a Self Hosted Script Based Alert Manager

## What is it?

The Balerter allows you to describe alert rules using scripts. This makes it possible to program rules of any complexity.

Balerter has internal support Lua for scripts writing.

Since **v0.10.0** you can use you preferred languages with HTTP Core API.
With Core API using you have to take care of running the scripts regularly. See more in [Core API](/core-api).

## Reasons for creating

Balerter was born from need to create complex business-metrics, which very hard to create declaratively.

A typical case:
- get historical data from first source
- get operative data from second source
- make needed calculation
- if our results are disturbing
- get meta-data from third source
- make a error message
- send a notification to messengers, etc
- repeat this steps every hour

There can be many such cases. Checking free space on hard disks or monitoring customer spends.
Checking the temperature in the refrigerator by http api or checking CPU load on servers.

In fact, you are not limited in your cases, as you are not limited in writing any programs with you programming language.

## What does the Balerter give?

- declare all data source in one place. You do not need to write DB connections in each script.
- provide API for access to any datasource, but not shadowing implementation details. You need to write SQL queries manually.
- can send notification to different targets: email, messengers, syslog. The list is regularly updated by your requests
- makes it easy to attach a chart image to a notification
- run your scripts with a defined interval

## Concepts

The main concept in Balerter is **Alert**.

Alert can be thought of as some object, which has the property: level. The level can have one of three values: `Error`, `Warning` and `Success`.
The level can be changed, but there can not be Alert with an undefined level. After creating an Alert, it has the `Success` level.
The moment of level change is a trigger for sending a notification.

An example.
We have a Lua script, that runs 1 times per minute.

```lua
-- @cron 0 * * * *

alert = require('alert')

alert.error('alert-id-1', 'Something went wrong')
```

After start of Balerter all Alerts have the `Success` status. On first run this script, command `alert.error('alert-id-1', ...)` set `Error` level for the Alert with id `alert-id-1`.
Since we have changed the level, you will receive a notification.

After minute a script will be run again and again will set the `Error` level for the Alert. But because the Alert already has the `Error` level, a notification will not be sent.

It will be repeated until the Alert level changed.

After run `alert.success('alert-id-1', ...)` (or `alert.warning`) in your script, the Alert level will be changed and you will receive a notification.

An example:

```lua
-- @cron 0 * * * * *

alert = require('alert')
prom = require('datasource.prometheus.prom1')

result = prom.query('sum(go_goroutines)')

-- Result value example:
-- {
--      1 = {
--          metrics = {}
--          timestamp = 1660055112
--          value = 957
--      }
-- }

if result[1].value > 1000 then
    alert.error('my-alert-id', 'too many goroutines')
else
    alert.ok('my-alert-id', 'goroutines count are ok')
end
```

> Calling `alert.error` does not send a notification. It changes the level value. A notification send when the level changes.
