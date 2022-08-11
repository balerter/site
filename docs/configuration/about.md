For start Balerter you must provide configuration file.

This file contains all datasources, channels, storages and other configuration options.

Balerter supports `yaml` and `hcl` formats for the configuration file.

## Names

For blocks, which must have `name`, you must use unique names for each item within sections with repeated items.

A correct example:
=== "HCL"
    ```tf
    datasources {
        clickhouse "db1" {
            // ...
        }
        clickhouse "db2" {
            // ...
        }
        postgres "db1" {
            // ...
        }
        postgres "db2" {
            // ...
        }
    }
    ```
=== "YAML"
    ```yaml
    datasources:
      clickhouse:
        - name: database1
          # ...
        - name: database2
          # ...
      postgres:
        - name: database1
          # ...
        - name: database2
          # ...
    ```
