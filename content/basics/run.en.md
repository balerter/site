---
title: "CLI flags"
date: 2020-02-04T16:20:36+03:00
draft: false
weight: 3
---

CLI flags:

```
-config=/path/to/config.yml         
 path to config file 
 default: config.yml

-logLevel=[LOG LEVEL]
 log level. ERROR, WARN, INFO or DEBUG
 default: INFO

-debug
 turn on debug mode for verbose logging
 default: false

-once
 once run scripts and exit
 default: false

-script=/path/to/script.lua
 ignore all script sources and runs only one script. Meta-tag @ignore will be ignored
 default: empty     
```