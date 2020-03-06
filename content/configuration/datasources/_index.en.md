---
title: "Datasource"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 3
---

In the `datasources` section describes data sources  

- [clickhouse](clickhouse) Clickhouse
- [prometheus](prometheus) Prometheus
- [postgres](postgres) Postgres
- [mysql](mysql) MySQL

```
datasources:
  clickhouse:
    - name: ch1
      host: domain.com
      port: 6440
      username: username
      password: password
      database: database
      ssl_cert_path: /path/to/cert.crt

  prometheus:
    - name: prom1
      url: domain.com
      basic_auth:
        username: username
        password: password

  postgres:
    - name: pg1
      host: domain.com
      port: 5432
      username: username
      password: password
      database: database
      ssl_mode: verify-full
      ssl_cert_path: /path/to/cert.crt

  mysql:
    - name: mysql1
      dsn: user:secret@tcp(127.0.0.1:3306)/database
```

