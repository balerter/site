---
title: "About"
date: 2020-02-04T16:32:46+03:00
draft: false
weight: 1
---

**Balerter** - it is an **Alert Manager**. 

Main Balerter purpose is opportunity for 'write easily hard alert rules'

For a simple alert, which firing on a http request limit, enough, for example, internal Grafana alerts.  

However, for more difficult tasks it is not enough. 
For example:
You wants select a historical data from a Database, then compare it with a current data. Then you calls an external API (over HTTP) and makes a decision about an Alert status. 

Exactly for same cases we did make the Balerter.

All business logic are describes in lua-scripts.

Inside a script you may:
- select data from different sources, for example: Prometheus or Postgres (etc)
- make any calculations and make a decision about an alert
- set level for an alert: Success, Warning or Error
- configure the behavior for notifications. For example: Warning Alerts send to duty engineer. Error Alerts send also to CTO
- make and attach a chart to a notification 