+++
title = "Содержание"
date = 2020-02-04T16:08:54+03:00
+++

![logo](logo.png)

Balerter это Self Hosted Script Based Alert Manager. 

> Английская версия документации содержит грамматические и лексические ошибки.
> Мы будем рады принять любую помощь в исправлении документации. Спасибо!

Fork me on the [github](https://github.com/balerter/balerter)

### Для чего?

Balerter появился из необходимости отслеживать сложные бизнес-метрики, которые очень трудно или невозможно описать декларативно. 

Типичный случай:
- получаем исторические данные из первого источника
- получаем оперативные данные из второго источника
- производим необходимые вычисления
- если вычисления нам говорят, что что-то пошло не так: 
- получаем мета-данные из третьего источника
- формируем сообщение об ошибке
- отправляем в доступные канали уведомлений
- повторяем эту проверку каждый час

Подобных кейсов может быть много. Они могут быть очень различные. Проверка свободного места на дисках или мониторинг затрат клиентов. Контроль температуры в холодильной камере или отслеживание нагрузки CPU на серверах. 

На самом деле вы никак не ограничены в области применения, как не ограничены в этом при создании программ на любом языке программирования.  

#### Чем это отличается от написания собственных скриптов на любом языке программирования?

Balerter помогает вам:

- позволяет описать все источники данных в одном месте, чтобы вам не пришлось в каждом вашем скрипте описывать, например, подключения к базам данных
- предоставляет API для доступа к различным источникам данных, но не скрывает детали реализации. Например, вы по-прежнему должны сами писать SQL-запросы
- умеет отправлять уведомления в различные цели: email, мессенджеры, syslog. Список постоянно растет по вашим запросам
- повозляет легко прикрепить к уведомлению изображение с графиком
- исполняет ваши скрипты с установленной периодичностью
- позволяет вашим отдельным скриптам обмениваться данными

### Содержание

- [Основы](basics)
    - [Установка](basics/install)
- [Конфигурация](configuration)
    - [Источники скриптов](configuration/scripts)
        - [Folder](configuration/scripts/folder)
    - [Источники данных](configuration/datasources)
        - [Clickhouse](configuration/datasources/clickhouse)
        - [Prometheus](configuration/datasources/prometheus)
        - [Postgres](configuration/datasources/postgres)
        - [MySQL](configuration/datasources/mysql)
        - [Loki](configuration/datasources/loki)
    - [Каналы](configuration/channels)
        - [Slack](configuration/channels/slack)
        - [Telegram](configuration/channels/telegram)
        - [Syslog](configuration/channels/syslog)
        - [Notify](configuration/channels/notify)
    - [Хранилища](configuration/storages)
        - [core](configuration/storages/core)
            - [file](configuration/storages/core/file)
        - [upload](configuration/storages/upload)
            - [S3](configuration/storages/upload/s3)
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
        - [Loki](core/datasource/loki)
    - [http](core/http)
- [Lua Модули](luamodules)
    - [Создание lua модуля](luamodules/new)
    - [Предустановленные модули](luamodules/presets)
        - [h](luamodules/presets#h)
        - [json](luamodules/presets#json)
- [Скрипты](scripts)
    - [Мета-теги](scripts/meta-tags)
- [API](api)
    - [Описание API](api/api)
- [Тестирование](testing)
- [Руководства](manuals)
    - [Подключение Slack](manuals/slack)
    - [Подключение Telegram](manuals/telegram)
- [Примеры](examples)
    - [Начальный](examples/00)
    - [Нагрузка на CPU](examples/01)
    - [Количество горутин (с графиком)](examples/02)
- [Список изменений](changelog)