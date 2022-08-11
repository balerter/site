=== "HCL"
    ```tf
    system = {
        jobWorkersCount = 32
        cronLocation = 'UTC'
    }
    ```
=== "YAML"
    ```yaml
    system:
        jobWorkersCount = 32
        cronLocation = 'UTC'
    ```

## jobWorkersCount

integer

> By default: 32

Allows redefining job workers count.

It can be useful if a large number of your scripts take a long time to execute

## cronLocation

string

> By default: "Local"

Allows setting timezone for the cron

For example: `Europe/Berlin`