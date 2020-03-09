+++
title = "Содержание"
date = 2020-02-04T16:08:54+03:00
+++

# Balerter

Balerter - система оповещений, основанная на скриптах

### Содержание

- [Основы](basics)
    - [О Balerter](basics/about)
    - [Установка](basics/install)
- [Конфигурация](configuration)
    - [Источники скриптов](configuration/scripts)
        - [Folder](configuration/scripts/folder)
    - [Источники данных](configuration/datasources)
        - [Clickhouse](configuration/datasources/clickhouse)
        - [Prometheus](configuration/datasources/prometheus)
        - [Postgres](configuration/datasources/postgres)
        - [MySQL](configuration/datasources/mysql)
    - [Каналы](configuration/channels)
        - [Slack](configuration/channels/slack)
        - [Telegram](configuration/channels/telegram)
        - [Syslog](configuration/channels/syslog)
    - [Хранилища](configuration/storages)
        - [S3](configuration/storages/s3)
    - [Глобальные](configuration/global)
- [Модули ядра](core)
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
- [Lua Модули](luamodules)
    - [О lua модулях](luamodules/about)
    - [Создание lua модуля](luamodules/new)
    - [Предустановленные модули](luamodules/presets)
        - [h](luamodules/presets#h)
        - [json](luamodules/presets#json)
- [Скрипты](scripts)
    - [Основы](scripts/basics)
    - [Мета-теги](scripts/meta-tags)
- [API](api)
    - [Описание API](api/api)
- [Руководства](manuals)
    - [Подключение Slack](manuals/slack)
    - [Подключение Telegram](manuals/telegram)
- [Примеры](examples)
    - [Нагрузка на CPU](examples/01)
    - [Количество горутин (с графиком)](examples/02)