+++
title = "The Content"
date = 2020-02-04T16:08:54+03:00
+++

![logo](logo.png)

Balerter is a Script Based Alert Manager

> English version of the documentation contains some grammatical and lexical typo and errors.
> We will be happy to accept any help in updating English version of the documentation.
> Thank you!

Fork me on the [github](https://github.com/balerter/balerter)

### The Content

- [Basics](basics)
    - [Installation](basics/install)
- [Configuration](configuration)
    - [Script Sources](configuration/scripts)
        - [Folder](configuration/scripts/folder)
    - [Data Sources](configuration/datasources)
        - [Clickhouse](configuration/datasources/clickhouse)
        - [Prometheus](configuration/datasources/prometheus)
        - [Postgres](configuration/datasources/postgres)
        - [MySQL](configuration/datasources/mysql)
        - [Loki](configuration/datasources/loki)
    - [Channels](configuration/channels)
        - [Slack](configuration/channels/slack)
        - [Telegram](configuration/channels/telegram)
        - [Syslog](configuration/channels/syslog)
        - [Notify](configuration/channels/notify)
    - [Storage](configuration/storages)
        - [core](configuration/storages/core)
            - [file](configuration/storages/core/file)
        - [upload](configuration/storages/upload)
            - [S3](configuration/storages/upload/s3)
    - [Global](configuration/global)
- [Core Modules](core)
    - [Log](core/log)
    - [KV](core/kv) (Key/Value)
    - [Chart](core/chart)
    - [Storage](core/storage)
        - [s3](core/storage/s3)
    - [Alert](core/alert)
    - [DataSoruce](core/datasource)
        - [Clickhouse](core/datasource/clickhouse)
        - [Postgres](core/datasource/postgres)
        - [Prometheus](core/datasource/prometheus)
        - [MySQL](core/datasource/mysql)
        - [Loki](core/datasource/loki)
    - [http](core/http)
- [Lua Modules](luamodules)
    - [Crate a lua module](luamodules/new)
    - [Preset modules](luamodules/presets)
        - [h](luamodules/presets#h)
        - [json](luamodules/presets#json)
- [Scripts](scripts)
    - [Meta-tags](scripts/meta-tags)
- [API](api)
    - [API](api/api)
- [Manuals](manuals)
    - [Connect to Slack](manuals/slack)
    - [Connect to Telegram](manuals/telegram)
- [Examples](examples)
    - [Simple](examples/00)
    - [CPU Load](examples/01)
    - [Goroutines count (with a chart)](examples/02)
- [Changelog](changelog)