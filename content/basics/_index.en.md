+++
title = "Basics"
date = 2020-02-04T16:07:19+03:00
weight = 1
pre = "<b>I. </b>"
+++

The main concept in Balerter is **Alert**. 

Alert can be thought of as some object, which has the property: level. The level can have one of three values: `Error`, `Warning` to `Success`.
The level can be changed, but there can not be Alert with an undefined level. After creating an Alert, it has the `Success` level.
The moment of level change is a trigger for sending a notification.

An example.
We have a script, that runs 1 times per minute.

```
alert = require('alert')

alert.error('alert-id-1', 'Something went wrong')
```

After start of Balerter all Alerts have the `Success` status. On first run this script, command `alert.error('alert-id-1', ...)` set `Error` level for the Alert with id `alert-id-1`.
Since we have changed the level, you will receive a notification.

After minute a script will be run again and again will set the `Error` level for the Alert. But because the Alert already has the `Error` level, a notification will not be sent.

It will be repeated until the Alert level changed.

After run `alert.success('alert-id-1', ...)` (or `alert.warning`) in your script, the Alert level will be changed and you will receive a notification.  

An example:

```
-- @interval 1m

alert = require('alert')

-- After first run this script an Alert has the 'Success' level.
-- And after by calling1 `alert.error` you change the level to `Error` and receive a notification 
alert.error('alert-id-1', 'message text')

-- after previous `alert.error` the level already has level `Error` and notification will not be sent
-- we just confirmed the `Error` level
alert.error('alert-id-1', 'message text')

-- we change the level to `Success` and get a notification
alert.success('alert-id-1', 'message text')

-- before exit from the script our Alert has the `Success` level
-- since the next run we call `alert.error`, set the `Error` level, get a notification and the history will be repeated 
```

Important! Calling `alert.error` does not send a notification. It changes the level value.
A notification send when the level changes.