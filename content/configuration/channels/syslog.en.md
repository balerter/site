---
title: "Syslog"
date: 2020-02-04T16:50:16+03:00
draft: false
---

JSON marshalled messaged will be send to syslog server

```
syslog:
  - name: default
    tag: balerter
    network: tcp
    address: 127.0.0.1:10515
    priority: 'EMERG|DAEMON'
```

### name 

> Required, Unique

Channel name

### tag

> Default: empty string

Syslog tag 

### network

> Default: empty string

Network type 
- `udp`
- `tcp`
- empty string for use local syslog server

### address

> Default: empty string

Server address

### priority

> Default: `EMERG`

Message priority

Format: `<SEVERITY>[|<FACILITI>]`

Severity:
- EMERG
- ALERT
- CRIT
- ERR
- WARNING
- NOTICE
- INFO
- DEBUG

Facility:
- KERN
- USER
- MAIL
- DAEMON
- AUTH
- SYSLOG
- LPR
- NEWS
- UUCP
- CRON
- AUTHPRIV
- FTP
- LOCAL0
- LOCAL1
- LOCAL2
- LOCAL3
- LOCAL4
- LOCAL5
- LOCAL6

For example:
```
priority: 'ALERT'
priority: 'ALERT|USER'
priority: 'INFO|LOCAL0'
```