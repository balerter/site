---
title: "Установка"
date: 2020-02-04T16:20:36+03:00
draft: false
weight: 1
---

## Докер

Официальный образ: [https://hub.docker.com/r/balerter/balerter](https://hub.docker.com/r/balerter/balerter)

Для простейшего запуска Balerter вам требуется передать ему конфигурационный файл

```
docker run \
    -v /path/to/config.yml:/opt/config.yml \
    balerter/balerter -config=/opt/config.yml

```

## Исходный код

Клонируем репозиторий на локальную машину и запускаем Balerter, указав конфигурационный файл

> Требуется Go версии 1.13 или выше

```
git clone https://github.com/balerter/balerter.git
cd balerter
go run ./cmd/balerter -config /path/to/config.yml
```