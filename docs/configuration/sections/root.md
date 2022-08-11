These options are not required and can be defined in the configuration file on top level

=== "HCL"
```tf
luaModulesPath = "./?.lua"
storageAlert = ""
storageKV = ""
```
=== "YAML"
```yaml
luaModulesPath: ./?.lua
storageAlert: ""
storageKV: ""
```

## luaModulesPath

string

> By default: ./?.lua;./modules/?.lua;./modules/?/init.lua;/modules/?.lua;/modules/?/init.lua

Semicolon separated list of paths to load lua modules from.

### `luaModulesPath`

> By default: "./?.lua;./modules/?.lua;./modules/?/init.lua;/modules/?.lua;/modules/?/init.lua"

Path to lua modules folder

### `storages`

Storage settings for core-modules.
You should set storage name, described in section [core storages](storages-core.md). Use a format:  
`<STORAGE_TYPE>.<STORAGE_NAME>`. Except for builtin storage - `memory`

> By default for all modules uses builtin value - `memory`

- alert: storage for Alerts data
- kv: storage for KV data

Example:
=== "HCL"
    ```tf
    storageAlert = "sqlite.mySqliteStorage"
    ```
=== "YAML"
    ```yaml
    storageAlert: sqlite.mySqliteStorage
    ```