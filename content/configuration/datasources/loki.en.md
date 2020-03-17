---
title: "Loki"
date: 2020-02-04T17:10:42+03:00
draft: false
weight: 5
---

```
name: loki1
url: domain.com
basicAuth:
  username: username
  password: password

```

### name 

> Required, Unique

Datasource name

```
local ds = require('datasource.loki.loki1')
```

### url

> Required

Request URI.
API path `/api/v1/...` will be added 

### basicAuth

Username and password, if Loki require Basic Auth