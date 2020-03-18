---
title: "Alert"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 5
---

**Alert** - is basic concept of Balerter 

Alert has unique ID and one of three possible statuses: `Success`, `Warning`, `Error`

By default status changing send notification. However, you can change this behavior.

Alerts are managed by their IDs. You manually define IDs and you should check their uniqueness. 

**Important!**, getting Alert by ID is global through all scripts 

On start all Alerts have status `Succes`

**Important!** Currenly supports only in-memory storage for alerts statuses. Its mean what after Balerter restart all Alerts will have `Success` status by default

---

```
local alert = require('alert')
```

### Parameters

All methods have one required and two not required arguments

1. Alert ID. Тип: `text`. Require
2. Notification message. Тип `text` 
3. Alert Options. Тип `table`

### Alert options

```
{
    quiet = <BOOL>,
    repeat = <UINT>,
    channels = <STRINGS>,
    fields = <STRINGS>
}

{
    quiet = true,
    repeat = 5,
    channels = {'channal-name-1', 'channel-name-2', ...},
    fields = {'field1', 'field2', ... }
}
```

#### quiet - suppress message on status change

#### repeat - notifications repeat

By default - 0. Set any non negative value N > 0, and notification will be send by every N check 

Example:

Our script, which run every 1 minute
```
-- @interval 1m

local alert = require('alert')

alert.error('alert-id', 'An error occured!`)
```

Because every alerts on start have status `Success`, on first script run alert will be changed to `Error` and you will get notification

On next runs, notifications will not be sent, because Alert already has status `Error'

Now change the script (add alert options):

```
alert.error('alert-id', 'An error occured!`, { repeat = 5 })
```

This mean, while status does not changed, every 5 runs notification will be sent

#### channels - notification channels

Redefine channels for send notifications

By default, notifications sent to all channels, registered in configuration

An example:

```
alert.error('alert-name-1', 'Alert Text', { channels = {'slack-seo'} })
```

#### fields - additional information

Additional information for an alert message.
Different channels may show it differently or not show!

An example:

```
alert.error('cpu-limit', 'High CPU', { ['fields'] = { 'cpu1 = 0.91', 'cpu2 = 0.97' } )
``` 

### Methods

#### `error(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Aliases: `on`, `fail`

Set status `Error`

An example:

```
alert.error('alert-id', 'An error accured')
alert.on('alert-id', 'User balance too low', { repeat = 5 })
alert.fail('alert-id', 'Service FOO is unavailable')
```

#### `warning(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Aliases: `warn`

Set status **Warning**

An example:

```
alert.warn('alert-id', 'RPS too low')
```

#### `success(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Aliases: `off`, `ok`

Set status **Success**

An example:

```
alert.success('alert-id', 'Serive is available')
alert.off('alert-id', '', { quiet = true })
alert.ok('alert-id', 'OK')
```


