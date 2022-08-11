??? success "Core API"
    This module available in Core API

**Alert** - is the basic concept of Balerter

Alert has unique ID (name) and one of three possible statuses: `Success`, `Warning`, `Error`

By default, status changing send notification. However, you can change this behavior.

Alerts are managed by their IDs. You manually define IDs, and you should check their uniqueness.

> Getting Alert by ID is global through all scripts

On start all Alerts have status `Succes`

## Usage:

```lua title="script.lua"
local alert = require('alert')
```

## Parameters

All methods have one required and two not required arguments

1. Alert ID. Type: `text`. Require
2. Notification message. Type `text`
3. Alert Options. Type `table`

## Alert options

```
{
    quiet = <BOOL>,
    resend = <UINT>,
    channels = <STRINGS>,
    image = <IMAGE_URL>,
    fields = <map[string]string>
}

{
    quiet = true,
    resend = 5,
    channels = {'channal-name-1', 'channel-name-2', ...},
    image = "http://placehold.it/200x200",
    fields = { foo = 'bar', baz = '42'}
}
```

### image

string

You can provide image URL for pass image to the channel.

For telegram channel you can use raw binary data for send image

```lua title="script.lua"
local img = chart.render(...)

alert.error('id', 'message text', { image = img } )
```

### quiet 

bool

suppress a message on status change. By default, `false`

### resend

int

notifications repeat (alias: `repeat`)

By default - 0. Set any non-negative value N > 0, and notification will be sent by every N check

Example:

Our script, which run every 1 minute

```lua title="script.lua"
-- @cron 0 * * * *

local alert = require('alert')

alert.error('alert-id', 'An error occured!`)
```

Because every alerts on start have status `Success`, on first script run alert will be changed to `Error` and you will get notification

On next runs, notifications will not be sent, because Alert already has status `Error'

Now change the script (add alert options):

```lua title="script.lua"
alert.error('alert-id', 'An error occured!`, { resend = 5 })
```

This is mean, while status does not change, every 5 runs notification will be sent

### channels

notification channels

Redefine channels for send notifications

By default, notifications sent to all channels, registered in configuration

An example:

```lua title="script.lua"
alert.error('alert-name-1', 'Alert Text', { channels = {'slack-seo'} })
```

### fields 

additional fields for the notification message

Fields will be attached to the message.

> `fields` option is not supported for channels: `notify`, `twilio` 

## Methods

### get

`get(<ALERT_NAME>) result, error`

Get an info about an alert

If an error occurred, it will be returns as second parameter

A response:

```
{
    name = <ALERT_NAME>
    level = <ALERT_LEVEL> (error|warning|success)
    last_change = <UNIX_TIMESTAMP>
    count = <INT>
}
```

An example:

```lua title="script.lua"
info = alert.get('alert-id')
```

### error

`error(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Aliases: `fail`

Set status `Error`

An example:

```lua title="script.lua"
alert.error('alert-id', 'An error accured')
alert.fail('alert-id', 'Service FOO is unavailable')
```

### warning

`warning(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Aliases: `warn`

Set status `Warning`

An example:

```lua title="script.lua"
alert.warn('alert-id', 'RPS too low')
```

### success

`success(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Aliases: `ok`

Set status `Success`

An example:

```lua title="script.lua"
alert.success('alert-id', 'Serive is available')
alert.ok('alert-id', 'OK')
```


