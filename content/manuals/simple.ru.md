---
title: "Базовый пример"
date: 2020-02-04T16:37:04+03:00
draft: false
weight: 1
---

В данной статье мы по шагам проработаем настройку системы и создание скрипта для следующей задачи:

> У нас есть Prometheus, который собирает какие-то метрики. Мы хотим отслеживать метрику `go_memstats_heap_objects`. Если значение превысит заданный нами порог, создадим алерт.   

### Конфигурирование

В первую очередь требуется создать файл конфигуации:

```
scripts:
  sources:
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'
        update_interval: 5s
datasources:
  prometheus:
    - name: prom1
      url: domain.com
channels:
  telegram:
    - name: tg1
      token: TELEGRAM-BOT-TOKEN
      chat_id: 100500
      proxy:

```

todo