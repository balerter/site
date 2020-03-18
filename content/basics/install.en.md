---
title: "Installation"
date: 2020-02-04T16:20:36+03:00
draft: false
weight: 1
---

## Docker

The official image: [https://hub.docker.com/r/balerter/balerter](https://hub.docker.com/r/balerter/balerter)

```
docker run \
    -v /path/to/config.yml:/opt/config.yml \
    balerter/balerter -config=/opt/config.yml

```

## Build from sources

Clone the repo and start the balerter (with the configuration file)

> Require Go 1.13 or later

```
git clone https://github.com/balerter/balerter.git
cd balerter
go run ./cmd/balerter -config /path/to/config.yml
```