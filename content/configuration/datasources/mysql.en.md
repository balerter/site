---
title: "MySQL"
date: 2020-02-04T17:10:48+03:00
draft: false
weight: 4
---

```
name: mysql1
dsn: user:secret@tcp(127.0.0.1:3306)/database
```

### name 

> Required, Unique

Datasource name 

```
local ds = require('datasource.postgres.mysql1')
```

### dsn

> Required

DSN (Data Source Name) for connect to DB

Format: `[username[:password]@][protocol[(address)]]/dbname[?param1=value1&...&paramN=valueN]`


> [golang packge](https://github.com/go-sql-driver/mysql) for more information about DSN

