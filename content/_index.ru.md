+++
title = "Содержание"
date = 2020-02-04T16:08:54+03:00
+++

# Balerter

Balerter - система оповещений, основанная на скриптах

### Содержание

- [Основы](basics)
    - [О Balerter](basics/about)
    - [Установка](basics/installation)
- [Конфигурация](configuration)
    - [Источники скриптов](configuration/scripts)
        - [Folder](configuration/scripts/folder)
    - [Источники данных](configuration/datasources)
        - [Clickhouse](configuration/datasources/clickhouse)
        - [Prometheus](configuration/datasources/prometheus)
        - [Postgres](configuration/datasources/postgres)
    - [Каналы](configuration/channels)
        - [Slack](configuration/channels/slack)
        - [Telegram](configuration/channels/telegram)
- [Модули ядра](core)
    - [Log](core/log)
    - [KV](core/kv) (Key/Value)
    - [Alert](core/alert)
    - [DataSoruce](core/datasource)
- [Скрипты](scripts)
    - [Основы](scripts/basics)
    - [Мета-теги](scripts/meta-tags)
- [Руководства](manuals)
    - [Подключение Slack](manuals/slack)
    - [Подключение Telegram](manuals/telegram)