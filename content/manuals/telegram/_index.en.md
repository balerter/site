---
title: "Telegram"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 3
---

1. In a telegram client find the bot with name `@BotFather` 

2. Creates new bot with a command `/newbot` 

3. Coping Access Token to the balerter configuration

4. We need to know 'chat id'. We can use the utility `tgtool` from balerter team

```
tgtool -token <TELEGRAM_BOT_TOKEN>
``` 

or

```
docker run --rm balerter/tgtool -token <TELEGRAM_BOT_TOKEN>
```

Send a message to you bot and you will see chat ID in the `tgtool` output

5. Mission Complete!