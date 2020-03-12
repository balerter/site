---
title: "Тип Slack"
date: 2020-02-04T16:50:16+03:00
draft: false
weight: 1
---

```
  slack:
    - name: slack-notification
      token: SLACK-APPLICATION-TOKEN
      channel: notification
```

### name 

> Обязательное поле, Уникальное значение

Название канала уведомлений, в том числе используется при логгировании

В названии могут использоваться латинские символы, цифры, знаки минуса и подчеркивания

### token

> Обязательное поле

Токен Slack приложения 

### channel

> Обязательное поле

Имя Slack канала
