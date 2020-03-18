+++
title = "Список изменений"
date = 2020-02-04T16:08:54+03:00
weight = 9
chapter = false
pre = "<b>IX. </b>"
+++

#### 2020-03-18 `v0.3.1`

- добавлена возможность устанавливать таймауты для источников данных в конфигурации

#### 2020-03-17 `v0.3.0`

- изменения в формате конфигурации
    - в секции scripts появился параметр updateInterval [подробнее](../configuration/scripts)
    - все параметры формата snake_case переведены в формат camelCase
        - datasources.clickhouse.ssl_cert_path -> datasources.clickhouse.sslCertPath
        - datasources.prometheus.basic_auth -> datasources.prometheus.basicAuth 
        - datasources.postgres.ssl_mode -> datasources.postgres.sslMode 
        - datasources.postgres.ssl_cert_path -> datasources.postgres.sslCertPath 
        - channels.telegram.chat_id -> channels.telegram.chatId 
        - global.send_start_notification -> global.sendStartNotification 
        - global.send_stop_notification -> global.sendStopNotification
- добавлена базовая поддержка источника данных: [Loki](../core/datasource/loki) 

#### 2020-03-16 `v0.2.0`

- поддержка постоянного хранилища для данных Алертов и KV
    - тип file

#### 2020-03-12 `v0.1.3`

- добавлен канал уведомлений notify - для отображения стандартных уведомлений ОС

#### 2020-03-11 `v0.1.2`

- убран метод API `/api/v1/config` для получения текущей конфигурации
- рефакторинг метода API `/api/v1/alerts`
    - изменен форматы выдачи
    - добавлена возможность указать фильтр по имени или уровню алерта
- внутренние оптимизации

#### 2020-03-09 `v0.1.1`

- исправлена ошибка в именовании константы модуля ядра
    - http.msethodTrace -> http.methodTrace

#### 2020-03-09 `v0.1.0`

- добавлен модуль ядра [http](../core/http)
- добавлен lua модуль [json](../luamodules/presets#json)