+++
title = "Основы"
date = 2020-02-04T16:07:19+03:00
weight = 1
pre = "<b>I. </b>"
+++

Главным понятием в balerter является - Alert.

Alert можно вопринимать как некоторый объект, который имеет свойство: уровень. Уровень может принимать одно из трех значений: Error, Warning или Success.
Значение уровня можно менять, но нельзя представить объект с неопределенным уровнем. В момент создания объекта по умолчанию устанавливается уровень Success.
Момент изменения уровня у Алерта является триггером для отправки уведомления. 

Покажем на примере.
Есть следующий скрипт, который выполняется 1 раз в минуту:

```
alert = require('alert')

alert.error('alert-id-1', 'Something went wrong')
```

При запуске balerter все Алерты имеют статус по умолчанию Success. При первом запуске данного скрипта, команда `alert.error('alert-id-1', ...)` устанавливает для Алерта с ID `alert-id-1` уровень `Error`.
Поскольку уровень изменился с Success на Error, вы получите уведомление об этом.

Через минуту скрипт выполнится опять и снова установит для вышеуказанного Алерта уровень `Error`. Но поскольку у него текущий уровень уже `Error`, то ничего не произойдет.

Сколько бы раз после этого не выполнялся скрипт со строкой  `alert.error`, уведомления не будет (на самом деле это поведение можно изменить, смотрите в документации по модулю [alert](../core/alert))

Но, как только в вашем скрипте встретится `alert.success('alert-id-1', ...)` (или `alert.warning`), то есть, как только изменится уровень данного Алерта, то вы получите уведомление об этом.

Исходя из вышеизложенного, следующий скрипт будет работать так:

```
-- @interval 1m

alert = require('alert')

-- При первом запуске Алерт имеет уровень Success, значит вызов alert.error поменяет уровень и вы получите уведомление
alert.error('alert-id-1', 'message text')

-- после выполнения предыдущей строки Алерт уже имеет уровень Error.
-- уведомленеия не будет. мы лишь подтвердили, что Алерт сейчас с уровнем Error
alert.error('alert-id-1', 'message text')

-- это командой мы меняем уровень на Success, значит вы получите уведомление
alert.success('alert-id-1', 'message text')

-- к моменту выхода из скрипта, Алерт имеет уровень Success
-- значит при следующем запуске и выполнении `alert.error` уровень снова поменяется, уведомление будет отправлено и все начнется с начала
```

Важно понимать, что вызов в скрипте `alert.error` не приводит к безусловной отправке уведомления, а служит для того, чтобы определить текущий уровень Алерта.
Отправка уведомления зависит от того, было изменение уровня в текущем моменте или нет.