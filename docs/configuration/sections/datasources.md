Section `datasources` defines data sources connections that are available for the Balerter.

Supported data sources:

- [clickhouse](#clickhouse)
- [prometheus](#prometheus)
- [postgres](#postgres)
- [loki](#loki)
- [mysql](#mysql)

## Clickhouse

=== "HCL"
    ```tf
    clickhouse "ch1" {
      host = "domain.com"
      port = 6440
      username = "username"
      password = "password"
      database = "database"
      sslCertPath = "/path/to/cert.crt"
      timeout = 3000
    }
    ```
=== "YAML"
    ```yaml
    clickhouse:
        - name: ch1
          host: domain.com
          port: 6440
          username: username
          password: password
          database: database
          sslCertPath: /path/to/cert.crt
          timeout: 3000 
    ```

### name

string

> Required, Unique

Datasource name

This name uses for connect to datasource from scripts. For example :

```lua title="script.lua"
local ds = require('datasource.clickhouse.ch1')
```

### host

string

> Required

Connection host

### port 

int

> By default: `6440`

Connection port

### username 

string

> By default: `default`

Connection username

### password 

string

Connection password

### database

string

> By default: `default`

Connection database

### sslCertPath 

string

Path to SSL cert. If empty, SSL do not use

### timeout

int

> By default: 5000 (5 sec)

Timeout, milliseconds

---

## Prometheus

=== "HCL"
    ```tf
    prometheus "prom1" {
      url = "domain.com"
      timeout = 3000
      basicAuth {
        username = "username"
        password = "password"
      }
    }
    ```
=== "YAML"
    ```yaml
    prometheus:
        - name: prom1
          url: domain.com
          timeout: 3000
          basicAuth:
            username: username
            password: password
    ```

### name 

string

> Required, Unique

Datasource name

```lua title="script.lua"
local ds = require('datasource.prometheus.prom1')
```

### url 

string

> Required

Request URI.
API path `/api/v1/...` will be added

### basicAuth 

Username and password, if Prometheus require Basic Auth

### timeout

int

> By default: 5000 (5 sec)

timeout, milliseconds

---

## Postgres

=== "HCL"
    ```tf
    postgres "pg1" {
      host = "domain.com"
      port = 5432
      username = "username"
      password = "password"
      database = "database"
      sslMode = "verify-full"
      sslCertPath = "/path/to/cert.crt"
      timeout = 3000
    }
    ```
=== "YAML"
    ```yaml
    postgres:
        - name: pg1
          host: domain.com
          port: 5432
          username: username
          password: password
          database: database
          sslMode: verify-full
          sslCertPath: /path/to/cert.crt
          timeout: 3000
    ```

### name

string

> Required, Unique

Datasource name

```lua title="script.lua"
local ds = require('datasource.postgres.pg1')
```

### host 

string

> Required

Connection host

### port

int

> By default: `5432`

Connection port

### username

string

> By default: `postgres`

Connection username

### password 

string

> By default: `postgres`

Connection password

### database

string

> By default: `postgres`

Connection database

### sslMode

string

> By default `disable`

SSL mode

### sslCertPath 

string

Path to SSL cert

### timeout

int

> By default: 5000 (5 sec)

timeout, milliseconds

---

## Loki

=== "HCL"
    ```tf
    loki "loki1" {
      url = "domain.com"
      timeout = 5000
      basicAuth {
        username = "username"
        password = "password"
      }
    }
    ```
=== "YAML"
    ```yaml
    loki:
        - name: loki1
          url: domain.com
          timeout: 5000
          basicAuth:
            username: username
            password: password
    ```

### name

string

> Required, Unique

Datasource name

```lua title="script.lua"
local ds = require('datasource.loki.loki1')
```

### url 

string

> Required

Request URI.
API path `/api/v1/...` will be added

### timeout

int

> By default: 5000 (5 sec)

timeout, milliseconds

### basicAuth 

Username and password, if Loki require Basic Auth

---

## MySQL

=== "HCL"
    ```tf
    mysql "mysql1" {
      dsn = "user:secret@tcp(127.0.0.1:3306)/database"
      timeout = 3000
    }
    ```
=== "YAML"
    ```yaml
    mysql:
        - name: mysql1
          dsn: user:secret@tcp(127.0.0.1:3306)/database
          timeout: 3000
    ```

### name 

string

> Required, Unique

Datasource name 

```lua title="script.lua"
local ds = require('datasource.postgres.mysql1')
```

### dsn

string

> Required

DSN (Data Source Name) for connect to DB

Format: `[username[:password]@][protocol[(address)]]/dbname[?param1=value1&...&paramN=valueN]`

An example: `user:secret@tcp(127.0.0.1:3306)/db`

> [golang packge](https://github.com/go-sql-driver/mysql) for more information about DSN

### timeout

int

> By default: 5000 (5 sec)

timeout, milliseconds


