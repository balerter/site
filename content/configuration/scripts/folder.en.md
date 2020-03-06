---
title: "Folder"
date: 2020-02-04T16:50:16+03:00
draft: false
---

```
name: scripts
path: /opt/scripts
mask: '*.lua'
update_interval: 5s
```

### name 

> Required, Unique

Script source name

### path

> Required

Path to folder  

### mask

> By default: `*.lua`

File mask

### update_interval

> By default: `10s`

With that interval Balerter check folder for any changes and reload if needed

A possible suffixes: "ns", "us" (or "µs"), "ms", "s", "m", "h".

Number must be not negative

> **Warning**! Too small value can cause high load