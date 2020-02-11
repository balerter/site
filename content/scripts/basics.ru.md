---
title: "Основы"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 1
---

Скрипты пишутся на языке **Lua 5.1**

С официальной документацией можно ознакомться [тут](http://www.lua.org/manual/5.1/) 

> Для разработчиков: в исходном коде используется Golang библиотка https://github.com/yuin/gopher-lua для исполнения Lua скриптов

Пример простого скрипта с подробными комментариями: (комментарии в Lua начинаются с двойного минуса `--`)

```
-- в начале скрипта можно указать некоторые мета-теги. Например, с помощью тега @interval можно указать частоту исполнения скрипта
-- все возможные варианты мета-тегов смотрите в соотвествующем разделе 
-- @interval 5m

-- в переменную sizeLimit запомним значение 1e9, которое будет в нашем случае означать 1Гб (1e9 в байтах) 
local sizeLimit = 1000000000

-- подключим модуль ядра Log для возможности вывода сообщений в лог сервиса
local log = require("log")
-- подключим источник данных типа Clickhouse с названием ch1 (он должен быть описан в файле конфигурации)
local ch1 = require("datasource.clickhouse.ch1")

-- получим ответ от Clickhouse на наш запрос
local res, err = ch1.query("SELECT sum(bytes) AS size FROM system.parts WHERE active")
-- если вернулась ошибка, то пишем сообщение в лог и выходим из скрипта
if err ~= nil then
    log.error("clickhouse 'ch1' query error: " .. err)
    return
end

-- из полученного результата берем первую запись (индексация массивов в Lua начинается с 1, а не с 0)
-- и в этой записи берем поле size (мы в запросе указали: ... AS size)
local currentSize = res[1].size

if currentSize > sizeLimit then
    -- если наше полученное значение выше нашего лимита, то
    -- устанавливаем для Алерта с идентификаторм clickhouse-disk-space статус Error
    -- если на момент вызова был другой статус, то будет отправлено уведомление с текстом 'Check disk space ...' 
    alert.error("clickhouse-disk-space", "Check disk space in Clickhouse cluster! Current busy: " .. tostring(currentSize))
else
    -- иначе устанавливаем для этого же Алерта статус Sucess
    -- если на момент вызова у алерта был другой статус (например, Error), то будет отправлено уведомление с текстом 'Clickhouse disk space - ok'  
    alert.success("clickhouse-disk-space", "Clickhouse disk space - ok")
end 
```