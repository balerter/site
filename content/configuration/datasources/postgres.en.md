---
title: "Postgres"
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
ssl_mode: verify-full
ssl_cert_path: /path/to/cert.crt
```

### name 

> Required, Unique

Datasource name

```
local ds = require('datasource.postgres.pg1')
```

### host

> Required

Connection host

### port

> By default: `5432`

Connection port

### username

> By default: `postgres`

Connection username

### password

> By default: `postgres`

Connection password

### database

> By default: `postgres`

Connection database

### ssl_mode

> By default `disable`

SSL mode

### ssl_cert_path

> By default: empty string

Path to SSL cert 
