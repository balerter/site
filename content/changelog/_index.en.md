+++
title = "Changelog"
date = 2020-02-04T16:08:54+03:00
weight = 10
chapter = false
pre = "<b>X. </b>"
+++

#### 2020-06-18 `v0.6.0`

- [ENHANCEMENT] added `Discord` channel [See more](../configuration/channels/discord)
- [ENHANCEMENT] added `Email` channel [See more](../configuration/channels/email)
- [ENHANCEMENT] new lua module: csv [See more](../luamodules/presets#csv)
- [ENHANCEMENT] allow setting CLI option '-config=stdin' for read the configuration file from os.stdin instead filesystem
- [FIX] do not start API server, if configuration option `global.API.Address` is empty
- add `pprof` endpoints for API server

#### 2020-04-23 `v0.5.0`

- added core module [runtime](../core/runtime)
- [FIX] fixed error with saving alerts data to the file storage
- added the CLI flag `-script` which allows quickly run the script [See more](../basics/run)
- added new ScriptSource provider - File [See more](../configuration/scripts/file)
- [FIX] disable sampling for the logger in the debug mode

#### 2020-04-03 `v0.4.0`

- ability to write tests [Testing](../testing)
- [BREAKING] removed alias-methods `alert.on` and `alert.off`
- [BREAKING] renames method `printTable` from lua module `h` to `print`. Now you call pass any value, not only table
- for obtain scripts from a source `folder`, script name will be defined as a filename without an extension. Before a path was been included 

#### 2020-03-23 `v0.3.2`

- added an API route '/liveness' [API](../api)
- added a method `get` for the core module `alert`. Use it for get an information about an alert [Alert](../core/alert)
- added a configuration item `Global.LuaModulesPath`. It allows redefine a folder for loading Lua modules [Configuration Global](../configuration/global)
- a base docker image was updated from alpine to debian:stretch-slim
- added an API route '/api/v1/kv' for obtain KV pairs from a storage [KV](../core/kv), [API](../api)

#### 2020-03-18 `v0.3.1`

- add timeouts for datasources in configuration

#### 2020-03-17 `v0.3.0`

- configuration schema changes
    - field 'updateInterval' in 'scripts' section [see more](../configuration/scripts)
    - all 'snake_case' fields now have 'camelCase' format
        - datasources.clickhouse.ssl_cert_path -> datasources.clickhouse.sslCertPath
        - datasources.prometheus.basic_auth -> datasources.prometheus.basicAuth 
        - datasources.postgres.ssl_mode -> datasources.postgres.sslMode 
        - datasources.postgres.ssl_cert_path -> datasources.postgres.sslCertPath 
        - channels.telegram.chat_id -> channels.telegram.chatId 
        - global.send_start_notification -> global.sendStartNotification 
        - global.send_stop_notification -> global.sendStopNotification 
- added basic support for datasource: [Loki](../core/datasource/loki) 

#### 2020-03-16 `v0.2.0`

- support a persistent storage for Alerts and KV data
    - type: file

#### 2020-03-12 `v0.1.3`

- added channel 'notify' for standard OS GUI notifications

#### 2020-03-11 `v0.1.2`

- removed API method `/api/v1/config`
- refactoring API method `/api/v1/alerts`
    - changed output format
    - added filters by 'name' and/or 'level'
- other optimizations

#### 2020-03-09 `v0.1.1`

- fix a typo in the `http` core module
    - http.msethodTrace -> http.methodTrace

#### 2020-03-09 `v0.1.0`

- added core module [http](../core/http)
- added lua module [json](../luamodules/presets#json)