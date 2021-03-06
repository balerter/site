---
title: "Alert"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 5
---

**Alert** - это базовая концепция сервиса. 

> В русской версии документации мы решили не переводить слово `Alert`, так как не удалось найти подходящего перевода в одно слово. Поэтому будем использовать `alert` или `алерт`

Alert имеет уникальный ID и один из трех статусов: `Success`, `Warning`, `Error`

По-умолчанию, изменение статуса Алерта инициирует отправку уведомления. Однако, вы всегда можете настроить это поведение, как вам удобно. Например: отправлять уведомление только при получении статуса `Error` и тихо менять статус во всех остальных случаях.

Управление Алертами просходит по их ID. Вы сами указываете идентификатор Алерта, поэтому вам следует следить, чтобы он был указан верно и был уникальным (когда вам это надо).

**Важно понимать**, что идентификация Алерта по ID является глобальной для всего сервиса. То есть, используя одинаковый ID в разных скриптах, вы будете обращаться к одному и тому же Алерту. 

При запуске сервиса все Алерты имеет статус `Success`

**Важно!** В данный момент поддерживается только in-memory имплементация хранилища Алертов. Это значит, что при перезапуске сервиса, все алерты буду иметь состояние по-умолчанию.

---

За управление Алертами отвечает одноименный модуль **alert**

```
local alert = require('alert')
```

### Параметры

Все методы этого модля принимают один обязательный и два необязательных параметра

1. Alert ID. Тип: `text`. Уникальный идентификатор Алерта. Обязательный параметр
2. Notification messafe. Тип `text`. Текст сообщения. Необязательный
3. Alert Options. Тип `table`. Опции. Необязательный

### Опции Алерта

Третьим параметром во всех методах данного модуля можно передать опции. 

Это Lua-table со следующими возможными полями:
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

#### quiet - тихая смена статуса

Установите в true, если вы хотите, чтобы при изменении статуса Алерта не отправлялось сообщение. По-умолчанию `false`. То есть, сообщение будет отправляться

#### repeat - повтор уведомлений

По-умолчанию 0. Установите в любое значение N > 0, чтобы при очередной проверке статуса Алерта - сообщение было отправлено.

Попробуем продемонстрировать использование этой опции на примере.

У вас есть следующий скрипт, который выполняется каждую минуту
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

#### `get(<ALERT_NAME>) result, error`

Получить информацию об алерте. 

Если произошла ошибка, она будет возвращена вторым параметром

Ответ:

```
{
    name = <ALERT_NAME>
    level = <ALERT_LEVEL> (error|warning|success)
    last_change = <UNIX_TIMESTAMP>
    count = <INT>
}
```

Пример:

```
info = alert.get('alert-id')
```

#### `error(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Алиасы: `fail`

Установить для алерта статус **Error**

Примеры:

```
alert.error('alert-id', 'An error accured')
alert.fail('alert-id', 'Service FOO is unavailable')
```

#### `warn(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

Установить для алерта статус **Warning**

Примеры:

```
alert.warn('alert-id', 'RPS too low')
```

#### `success(<ALERT_NAME>[, <ALERT_MESSAGE>[, <ALERT_OPTIONS>]])`

> Алиасы: `ok`

Установить для алерта статус **Success**

Примеры:

```
alert.success('alert-id', 'Serive is available')
alert.ok('alert-id', 'OK')
```


