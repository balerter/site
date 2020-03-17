+++
title = "Changelog"
date = 2020-02-04T16:08:54+03:00
weight = 9
chapter = false
pre = "<b>IX. </b>"
+++

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