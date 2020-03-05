---
title: "Тип MySQL"
date: 2020-02-04T17:10:48+03:00
draft: false
weight: 4
---

```
name: mysql1
dsn: user:secret@tcp(127.0.0.1:3306)/database
```

### name 

> Обязательное поле, Уникальное значение среди источников данных этого типа

Название источника данных

В названии могут использоваться латинские символы, цифры и знак подчеркивания

По этому имени вы будете обращаться из скрипта, например:

```
local ds = require('datasource.postgres.mysql1')
```

### dsn

> Обязательное поле

Строка (Data Source Name) для подключения к БД

Формат: `[username[:password]@][protocol[(address)]]/dbname[?param1=value1&...&paramN=valueN]`


> В описании [используемой библиотеки](https://github.com/go-sql-driver/mysql) можно посмотреть подробнее про построение DSN


## Информация

На данный момент не поддерживаются поля GEOMETRY, ENUM

Если вам необходима их поддержка, создайте [issue на github](https://github.com/balerter/balerter/issues)