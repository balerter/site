---
title: "Тип Postgres"
date: 2020-02-04T17:10:48+03:00
draft: false
weight: 3
---

```
name: pg1
host: domain.com
port: 5432
username: username
password: password
database: database
sslMode: verify-full
sslCertPath: /path/to/cert.crt
```

### name 

> Обязательное поле, Уникальное значение среди источников данных этого типа

Название источника данных

В названии могут использоваться латинские символы, цифры и знак подчеркивания

По этому имени вы будете обращаться из скрипта, например:

```
local ds = require('datasource.postgres.pg1')
```

### host

> Обязательное поле

Хост для подключения к БД

### port

> По-умолчанию `5432`

Порт для подключения к БД

### username

> По-умолчанию `postgres`

Имя пользователя для подключения к БД

### password

> По-умолчанию `postgres`

Пароль для подключения к БД

### database

> По-умолчанию `postgres`

Имя БД для подключения

### sslMode

> По-умолчанию `disable`

SSL режим

### sslCertPath

> По-умолчанию пустая строка

Пусть к SSL сертификату для подключения к БД
