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

Так как, при старте сервиса все Алерты имееют статус по-умолчанию `Success`, то при первом запуске скрипта и измениии статуса на `Error` вы получите уведомление.

При последующих запусках скрипта, уведомления об ошибке отправляться (повторяться) не будут, так как Алерт уже имеет статус `Error` и этот статус не меняется.

Теперь в скрипте напишем следующее:

```
alert.error('alert-id', 'An error occured!`, { repeat = 5 })
```

Это будет означать, что, пока статус не поменялся, каждый пятый вызов этого метода будет приводить к отправке сообщения. То есть, каждые пять минут вы будете получать уведомление о ошибке, пока статус не поменяется.

#### channels - каналы для отправки уведомлений

Позволяет переопределить список каналов, куда будет отправлено уведомление.

По-умолчанию берутся все каналы, описанные в файле конфигурации. Для всех Алертов конкретного скрипта можно переопределить список каналов с помощью мета-тега `@channels`. 
И, наконец, в опциях Алерта можно переопределить каналы для этого конкретного алерта

Например:

```
alert.error('alert-name-1', 'Alert Text', { channels = {'slack-seo'} })
```

#### fields - дополнительные поля в сообщении

При отображении уведомления, помимо самого текста уведомления, можно добавить информация в виде массива строк, которая будет так же видна в сообщении.
Конкретное отображение зависит от типа канала. То есть, например, в Slack и в Email будет разный вид. Но общая концепция "Дополнительная инфорация в виде массива строка" сохраняется

Пример:

```
alert.error('cpu-limit', 'High CPU', { ['fields'] = { 'cpu1 = 0.91', 'cpu2 = 0.97' } )
``` 

### Методы

#### `error(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Алиасы: `on`, `fail`

Установить для алерта статус **Error**

Примеры:

```
alert.error('alert-id', 'An error accured')
alert.on('alert-id', 'User balance too low', { repeat = 5 })
alert.fail('alert-id', 'Service FOO is unavailable')
```

#### `warn(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

Установить для алерта статус **Warning**

Примеры:

```
alert.warn('alert-id', 'RPS too low')
```

#### `success(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Алиасы: `off`, `ok`

Установить для алерта статус **Success**

Примеры:

```
alert.success('alert-id', 'Serive is available')
alert.off('alert-id', '', { quiet = true })
alert.ok('alert-id', 'OK')
```


