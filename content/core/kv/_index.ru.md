---
title: "KV"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 2
---

Модуль `kv` _(key/value)_ используется для хранения пар ключ-значение.

Это позволяет вашим скриптам хранить какие-то данные между запусками. Или даже обмениваться данными между различными скриптами

Использование:

```
local kv = require('kv')
```

> Все ключи и значения являются строками. Если необходимо, вы можете преобразовывать их в своих скриптах.
> Но имейте ввиду, даже если при сохранении вы передали число, при получении вы получите строку.

### Методы

#### `put(<NAME>, <VALUE>) error`

Сохранить значение `VALUE` с ключом `NAME`

Если значение с таким ключом уже существует, будет возвращена ошибка

```
local err = kv.put('key', 'value')
if err ~= nil then
    print('unable to put the variable in KV: ' .. err)
    return
end
```

#### `get(<NAME>) string, error`

Получить значение по ключу `NAME`

Если запись с таким ключом не существует, будет возвращена ошибка

```
local value, err = kv.get('key')
if err ~= nil then
    print('a variable not exists in KV: ' .. err)
    return
end

print('value: ' .. value)
```

#### `upsert(<NAME>, <VALUE>) error`

Сохранить или обновить значение `VALUE` с ключом `NAME`

Если значение с таким ключом уже существует, оно будет перезаписано новым значением

```
local err = kv.put('key', 'value')
kv.upsert('key', 'new value')
```

> Для **in-memory** имплементации метод `upsert` никогда не возвращает ошибку. Однако это может поменяться в будущем при использованиим других имплементаций модуля KV

#### `delete(<NAME>) error`

Удалить запись с ключом `NAME`

Если запись с таким ключом не существует, будет возвращена ошибка

```
local value, err = kv.delete('key')
if err ~= nil then
    print('a variable not exists in KV: ' .. err)
    return
end

print('variable "key" has been deleted')
```
