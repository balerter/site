Section `scripts` describes scripts sources.

You can to define any number of scripts sources any types

## Example

=== "HCL"

    ```tf
    scripts {
      updateInterval = 5000
      folder "scripts"{
        path = "/opt/scripts"
        mask = "*.lua" 
      }
      file "demo1" {
        filename = "/path/to/demo.lua"
        disableIgnore = false
      }
      postgres "pg1" {
        host = "domain.com"
        port = 5432
        username = "username"
        password = "password"
        database = "database"
        sslMode = "verify-full"
        sslCertPath = "/path/to/cert.crt"
        query = "SELECT name, body FROM scripts"
      }
    }
    ```
=== "YAML"

    ```yaml
    scripts:
      updateInterval: 30000
      folder:
        - name: scripts
          path: /opt/scripts
          mask: '*.lua'
      file:
        - name: demo1
          filename: /path/to/demo.lua
          disableIgnore: false
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
          query: "SELECT name, body FROM scripts"
    ```

## Common

### updateInterval

int

> By default: 60000 (1 minute)

An interval for check changes in script sources, milliseconds.

---

## Type `file`

=== "HCL"
    ```tf
    file "demo1" {
      filename = "/path/to/demo.lua"
      disableIgnore = false
    }
    ```
=== "YAML"
    ```yaml
    file:
      - name: scripts
        filename: /opt/scripts/demo.lua
        disableIgnore: false
    ```

### name

string

> Required, Unique

Script source name

### filename 

string

> Required

Path to the script  

### disableIgnore 

bool

> By default: `false`

If `true`, meta-tag `@ignore` will be ignored

---

## Type `folder`

=== "HCL"
    ```tf
    folder "scripts"{
      path = "/opt/scripts"
      mask = "*.lua" 
    }
    ```
=== "YAML"
    ```yaml
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'
    ```

### name 

string

> Required, Unique

Script source name

### path

string

> Required

Path to folder  

### mask

string

> By default: `*.lua`

File mask

---

## Type `postgres`

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
      query = "SELECT name, body FROM scripts"
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
        query: "SELECT name, body FROM scripts"
    ```
### name

string

> Required, Unique

Script source name

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

> By default: empty string

Path to SSL cert

### timeout

int

> By default: 5000

timeout, milliseconds

### query

string

Query for scripts select.

You must return exactly two string fields!
First field for script name, and second field for script body.

Example:

```sql
SELECT name, body FROM scripts
```