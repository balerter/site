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
sslMode: verify-full
sslCertPath: /path/to/cert.crt
timeout: 3s
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

### sslMode

> By default `disable`

SSL mode

### sslCertPath

> By default: empty string

Path to SSL cert 

### timeout

> By default: 5s string

timeout
 
