??? success "Core API"
    This module available in Core API

The `storage` module allows upload data to remote storage, described in configuration

Usage:

```lua title="script.lua"
local storage = require('storage.<TYPE>.<NAME>')
```
 
- type - storage type
    - s3
- name - storage name from configuration


An example:

A configuration file
```yaml
storages:
  s3:
    - name: dev
      ...
```

A script
```lua title="script.lua"
local s3 = require('storage.s3.dev')
```

## s3

The `storage.s3` module allows upload data to remote storage with Amazon S3 compatible API

## Methods

### uploadPNG 

`uploadPNG(data[, <FILENAME>]) imageURL, error`

Upload `PNG` image and get public URL

If an error occurred, it will be returned as second value

If filename is not defined, it will be generated.
You should provide filename without an extension
If your filename will be having suffix `.png`, `.jpg` или `.jpeg`, it will be trimmed

An example:

```lua title="script.lua"
local storage = require('storage.s3.dev')

local data = 'SOME_IMAGE_DATA_FROM_MODULE_CHART'

local link, err = storage.uploadPNG(data)
```

### A public link

A public link builds with format:

```
https://<BUCKET>.<ENDPOINT>/<FILENAME>
```