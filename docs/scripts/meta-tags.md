In the script head you can define some meta-tags

```lua title="script.lua"
-- @cron 0 * * * * *
-- @ignore

local log = require('log')
```

Every meta-tag has a format: `@<TAG_NAME> [<TAG_OPTIONS>]`

All meta-tags should be exactly in the head of script

Any not empty not comment string will interrupt meta-tags parsing

```lua title="script.lua"
-- You CAN place comments without tags
-- @cront */10 * * * * * (comment in the meta-tag line NOT ALLOWED)
--
-- empty comment string ALLOWED


-- also ALLOWED empty strings

local a = 10

-- @ignore
-- this tag will not be parsing, because we write not empty not comment string above
```  

## Meta-tags

### cron

`@cron <EXPRESSION>`

If not defined, used default value: 1 minutes (0 * * * * *)

The cron expression have 6 sections:

```
Second, Minute, Hour, Day-of-Month, Month, Day-of-week
```

[Link to the Wikipedia](https://en.wikipedia.org/wiki/Cron)

### ignore 

`@ignore`

If this meta-tag is present, this script will not be run

An example:

```lua
-- @ignore
```

### name 

`@name <SCRIPT NAME>`

Script name for logging

By default, use filename

An example:

```lua
-- @name script1
```

### channels 

`@channels <CHANNEL NAME 1>,<CHANNEL NAME 2>,...`

Allows redefining channels for send notifications.

By default, notifications send to all channels, described in the configuration

You can define multiply channel in comma-separated string

An example:

```lua
-- @channels slack-manager,email-ceo
```

### test 

`@test <MAIN_SCRIPT_NAME>`

Mark this script as 'Test' for the script with name `<MAIN_SCRIPT_NAME>`

This script will be running only with `balerter/test` tool. With `balerter` this script will be ignored

```lua
-- @name demo-test
-- @test demo

test = require('test')
```

### timeout 

`@timeout <TIME DURATION>`

Set timeout for the script.

By default, 1 hour

```lua
-- @timeout 30s
```

### escalate 

`@escalate NUM:CHANNEL,CHANNEL NUM:CHANNEL ...`

Define escalation rules for the script.

- NUM - alert fire count
- CHANNEL - channels name, comma-separated string

Rules are space-separated string
