---
title: "Clickhouse"
date: 2020-02-04T17:10:36+03:00
draft: false
weight: 1
---

```
name: ch1
host: domain.com
port: 6440
username: username
password: password
database: database
sslCertPath: /path/to/cert.crt
```

### name 

> Required, Unique

Datasource name

This name uses for connect to datasource from script. For example:

```
local ds = require('datasource.clickhouse.ch1')
```

### host

> Required

Connection host

### port

> By default: `6440`

Connection port

### username

> By default: `default`

Connection username

### password

> By default: empty string

Connection password

### database

> By default: `default`

Connection database

### sslCertPath

> By default: empty string

Path to SSL cert. If empty, SSL do not use
