---
title: "Datasource"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 3
---

In the `datasources` section describes data sources  

- [Clickhouse](clickhouse) 
- [Prometheus](prometheus) 
- [Postgres](postgres) 
- [MySQK](mysql) 
- [Loki](loki)

```
datasources:
  clickhouse:
    - name: ch1
      host: domain.com
      port: 6440
      username: username
      password: password
      database: database
      sslCertPath: /path/to/cert.crt
      timeout: 3s

  prometheus:
    - name: prom1
      url: domain.com
      basicAuth:
        username: username
        password: password

  postgres:
    - name: pg1
      host: domain.com
      port: 5432
      username: username
      password: password
      database: database
      sslMode: verify-full
      sslCertPath: /path/to/cert.crt
      timeout: 3s

  mysql:
    - name: mysql1
      dsn: user:secret@tcp(127.0.0.1:3306)/database

  loki:
    - name: loki1
      url: domain.com
      timeout: 5s
      basicAuth:
        username: username
        password: password
```

