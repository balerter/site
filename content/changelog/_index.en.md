+++
title = "Changelog"
date = 2020-02-04T16:08:54+03:00
weight = 9
chapter = false
pre = "<b>IX. </b>"
+++


#### 2020-03-11 `v0.1.2`

- removed API method `/api/v1/config`
- refactoring API method `/api/v1/alerts`
    - changed output format
    - added filters by 'name' and/or 'level'
- other optimizations

#### 2020-03-09 `v0.1.1`

- fix a typo in the `http` core module
    - http.msethodTrace -> http.methodTrace

#### 2020-03-09 `v0.1.0`

- added core module [http](../core/http)
- added lua module [json](../luamodules/presets#json)