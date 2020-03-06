---
title: "Prometheus"
date: 2020-02-04T17:10:42+03:00
draft: false
weight: 2
---

```
name: prom1
url: domain.com
basic_auth:
  username: username
  password: password

```

### name 

> Required, Unique

Datasource name

```
local ds = require('datasource.prometheus.prom1')
```

### url

> Required

Request URI.
API path `/api/v1/...` will be added 

### basic_auth

Username and password, if Prometheus require Basic Auth