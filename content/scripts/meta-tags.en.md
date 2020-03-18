---
title: "Meta-tags"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 2
---

In the script head you can defined some meta-tags

```
-- @interval 10s
-- @ignore

local log = require('log')
...

```


Every meta-tag has a format: `@<TAG_NAME> [<TAG_OPTIONS>]`

All meta-tags should be exactly in the head of script 

Any not empty not comment string will be interrupted meta-tags parsing

```
-- You CAN place comments without tags
-- @interval 10s (comment in the meta-tag line NOT ALLOWED)
--
-- empty comment string ALLOWED


-- also ALLOWED empty strings

local a = 10

-- @ignore
-- this tag will not be parsing, because we write not empty not comment string above
```  

### Meta-tags

#### `@interval <TIME INTERVAL>`

Run script Interval
If not defined, used default value: 60 seconds

Possible suffixes for a value: "ns", "us" (or "µs"), "ms", "s", "m", "h".


An example:
```
-- @interval 10s
-- @interval 5m
```
                                    
#### `@ignore`

If this meta-tag is present, this script will not be run

An example:
```
-- @ignore
```


#### `@name <SCRIPT NAME>`

Script name for logging

By default use filename

An example:
```
-- @name script1
```

#### `@channels <CHANNEL NAME 1>,<CHANNEL NAME 2>,...`

Allows redefine channels for send notifications.

By default, notifications send to all channels, described in the configuration

An example:
```
-- @channels slack-manager,email-ceo
```

#### An example

```
-- multi meta example

-- @name MyScript
-- @interval 5m

-- @channels slack-ceo,telegram-ceo

...
```