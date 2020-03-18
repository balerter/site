---
title: "Slack"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 2
---

1. Create an application on the page `https://api.slack.com/apps?new_app=1`

2. In the section `OAuth & Permissions` `https://api.slack.com/apps/<ID>/oauth` add scopes 
    - `chat:write`
    - `incoming-webhook`

![Example](s1.png)

3. Install an application to the workspace, select a channel for notifications and coping `OAuth Access Token`

4. In slack application add this application to the channel (`Add an app`)

5. Use OAuth in the balerter configuration

6. Mission Complete