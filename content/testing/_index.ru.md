+++
title = "Тестирование"
date = 2020-02-04T16:08:54+03:00
weight = 7
chapter = false
pre = "<b>VII. </b>"
+++

Balerter позволяет вам тестировать свои скрипты!

Для этого вы можете писать отдельные тестовые скрипты и использовать в них встроенный модуль test. Запуск тестов осуществляется с помощью отдельной утилиты balerter/test с подключением того же файла конфигурации, который вы используете для запуска balerter с основными скриптами

Скрипты будут получены из источников скриптов, описанных в файле конфигурации. А все запросы к источникам данных будут переопределены моками. Подключения к базам данных и тд выполняться не будут.

### Написание тестов

Используется следующая концепция: отдельный тестовый файл для отдельного скрипта

Пример:

Файл, который мы будем тестировать:
```
-- @name demoscript

log = require('log')

log.error('foo')
log.info('bar')
```

Как видим, логика очень проста - мы просто пишем в лог два сообщения.

Теперь напишем и разберем тест-файл:

```
-- @name demoscript-test
-- @test demoscript

test = requeire('test')

test.log().on('error', 'foo').response()
test.log().on('info', 'bar').response()

test.log().assertCalled('error', 'foo')
test.log().assertCalled('info', 'bar')
test.log().assertNotCalled('warn', 'baz')
```

Мета-тегом `@test` мы указали сразу две вещи: 1. Это файл с тестом и он не должен выполняться при обычном запуске, 2. Мы тестируем файл с именем `demoscript`. [Подробнее о мета тегах](../scripts/meta-tags)

### Модуль `test`

> Модуль `test` может быть подключен только в срипте с тестом, который имеет мета-тег `@test`

Модуль позволяет:
- указать данные, которые дожны возвращаться при вызове других модулей или запросов к источникам данных в главном скрипте. Если вы в главном скрипте вызываете, например, `log.error('foo')` но в файле теста не уазали, что надо вернуть в ответ на этот вызов (пусть даже nil) - то будет зафиксирована ошибка выполнения теста
- описать Asserts для вызовов, которые вы ожидаете или нет. В случае несовпадения, будет ошибка выполнения теста 

Методы модуля можно описать так:
- `test.<MODULE>.on(<METHOD>, [<ARG>, <ARG>, ...]).response([<ARG>, <ARG>, ...])`
- `test.<MODULE>.assertCalled(<METHOD>, [<ARG>, <ARG>, ...])`
- `test.<MODULE>.assertNotCalled(<METHOD>, [<ARG>, <ARG>, ...])`

`<MODULE>` - это может быть `datasource(<DATASOURCE_NAME>)` для источников данных. Например `test.datasource('postgres.prod')`. 

Или обращение к модулям ядра:
- log()
- http()
- chart()
- alert() 
- kv() 

Например:

```
-- укажем ответ (в нашем случае - ничего) для вызова log.error('error message') в главном скрипте
test.log().on('error', 'error message').response()

-- проверяем, что будет вызов alert.error('alert-id', 'alert message')
test.alert().assertCalled('error', 'alert-id', 'alert message')

-- указываем, что вернуть на вызов ch1.query('SELECT * FROM users'), где ch1 = require('datasource.clickhouse.ch1')
test.datasource('clickhouse.ch1').on('query', 'SELECT * FROM users').response({ { id = 1, name = 'John' } })
```

> Обратите внимание! Даже если вызов ничего не возвращает, например `log.info(...)` вы все равно должны описать в скрипе этот вызов `test.log().on('info', 'message').resoponse()` чтобы система зарегистрировала его и знала, как на него реагировать 

### Запуск тестов

Для запуска используется утилита test, входящая в пакет balerter.

Пример запуска из докер образа:

```
docker run --rm \
    -v /path/to/config.yml:/opt/config.yml \
    -v /path/to/scripts:/opt/scripts \
    balerter/test -config=/opt/config.yml
```

Если произошла ошибка запуска, код завершения приложения будет равен 1. Если тесты завершилисть с ошибкой, код будет равен 2. При корректном прохождении тестов, код равен 0

Пример выдачи:
```
[FAIL]  [demo-test]     [alert] method 'success' with args [alert-id,All OK] was called, but should not
[PASS]  [demo-test]     [alert] method 'error' with args [alert-id Error get key] was not called
[PASS]  [demo-test]     [kv]    method 'get' with args [foo] was called
[FAIL]  [demo-test]     [result]        FAIL
```

Первая колонка - результат строки. Вторая - имя скрипта с тестом. Третья - название модуля. Далее идет сообщение.
Если в названии модуля указано `result` - это итоговый результат для скрипта с тестом

Скрипты для выдачи выше:
```
-- main script
-- @name demo

alert = require('alert')
kv = require('kv')

v, err = kv.get('foo')

if err ~= nil then
    alert.error('alert-id', 'Error get key')
else
    alert.success('alert-id', 'All OK')
end
```

```
-- test script
-- @test demo
-- @name demo-test

test = require('test')

test.kv().on('get', 'foo').response(42, nil)
test.kv().assertCalled('get', 'foo')

test.alert().on('success', 'alert-id', 'All OK').response()
test.alert().assertNotCalled('success', 'alert-id', 'All OK')
test.alert().assertNotCalled('error', 'alert-id', 'Error get key')
```

### Планы по доработке системы тестирования

#### Возможность указать test.AnyValue для Ассертов или on...response

Например, регистрация ответа на вызов `log.error(<ЛЮБОЕ ЗНАЧЕНИЕ>)`
```
test.log().on('error', test.AnyValue).response()
```

#### Возможность использовать функции группировки тестов для нескольких изолированных запусков

Пример тест-файла:
```
test = require('test')

test.group('group name 1', function(t)
    t.log().on('error', 'message').response()
    t.alert().assertCalled('error', 'alert-id', 'message') 
end)

test.group('group name 2', function(t)
    t.group('group name 2-1', function(t2)
        t2.log().on('error', 'message').response()
        t2.alert().assertCalled('error', 'alert-id', 'message') 
    end)

    t.group('group name 2-2', function(t2)
        t2.log().on('error', 'message').response()
        t2.alert().assertCalled('error', 'alert-id', 'message') 
    end)
end)
```

В этом случае будет выполнено тестирование для каждой функции отдельно

> Голосуйте за соответствующие issues на [github](https://github.com/balerter/balerter) проекта или создавайте новые!