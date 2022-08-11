If you can to notify specific channels if the alert still not resolve, you can use `@escalate` meta-tag for scripts.

A script example:

```lua
-- @cron 0 */10 * * * *
-- @escalate 5:telegram_cto,slack_manager 10:telegram_ceo
-- @channels slack_ingeneer

...

alert.error('script-id', 'Alert message')
```

By default, this script sent alerts to `slack_ingeneer` channel.

In this example script will be run every 10 minutes and if the alert is not resolved, 
alert will be sent to the channels `telegram_cto` and `slack_ingeneer` on 5 script run (if error state is `error`). And alert will be sent to `telegram_ceo` on 10-th script run.


## Escalate options

`--@escalate num:channel,channel num:channel`

`num` - number of script alerts run `error` before alert will be sent to the channels

After `num:` you can define channels list, separated by `,`

Escalate rules are space-separated, so you can define multiple rules.
