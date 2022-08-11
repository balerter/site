Core storage use for storing Alerts and KV data

It supports 2 types: `sqlite` and `postgres`

For each of these types you should define tables and fields for storing Alerts and KV data

**You do not have direct access to these storages from your scripts**

=== "HCL"
    ```tf
    storagesCore {
      sqlite "mySqliteStorage" {
        path = "/path/to/file"
        timeout = 1000
        tableKV {
          create = true
          table = "kv"
          fields {
            key = "key"
            value = "value"
          }
        }
        tableAlerts {
          create = true
          table = "alerts"
          fields {
            name = "id"
            level = "level"
            count = "count"
            createdAt = "created_at"
            updatedAt = "updated_at"
          }
        }
      }
      
      postgres "pg1" {
        host = "domain.com"
        port = 5432
        username = "username"
        password = "password"
        database = "database"
        sslMode = "verify-full"
        sslCertPath = "/path/to/cert.crt"
        timeout = 3000
        tableKV = {} // same as sqlite above
        tableAlerts = {} // same as sqlite above
      }
    }
    ```
=== "YAML"
    ```yaml
    storagesCore:
      sqlite:
        - name: mySqliteStorage
          path: /path/to/file
          timeout: 1000
          tableKV:
            create = false
            table: "kv"
            fields:
              key: key
              value: value
          tableAlerts:
            create = false
            table: "alerts"
            fields:
              name: id
              level: level
              count: count
              createdAt: created_at
              updatedAt: updated_at
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
          tableKV: ... same as sqlite above
          tableAlerts: ... same as sqlite above
    ```

If you want to create tables by Balerter, you should use `create = true`. By default, this options is `false`