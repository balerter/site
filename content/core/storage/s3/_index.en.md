---
title: "s3"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 1
---

The `storage.s3` module allows upload data to remote storage with Amazon S3 compatible API

### Methods

#### `uploadPNG(data[, <FILENAME>]) imageURL, error`

Upload `PNG` image and get public URL

If an error occurred, it will be returned as second value

If filename is not defined, it will be generated.
You should provide filename without an extension
If your filename will be have suffix `.png`, `.jpg` или `.jpeg`, it will be trimmed

An example:

```
local storage = require('storage.s3.dev')

local data = 'SOME_IMAGE_DATA_FROM_MODULE_CHART'

local link, err = storage.uploadPNG(data)

```

### A public link

A public link builds with format:

```
https://<BUCKET>.<ENDPOINT>/<FILENAME>
```