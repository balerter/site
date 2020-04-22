---
title: "Runtime"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 10
---

Module `runtime` allows you to get an information about the Balerter runtime

Usage:

```
local runtime = require('runtime')
```

### Methods

#### `logLevel() string`

Get a logger level value (CLI flag `-logLevel`) 

```
local logLevel = runtime.logLevel()
// INFO
```

#### `isDebug() bool`

True, if the CLI flag `-debig` has been defined

```
print(runtime.isDebug())
```

#### `isOnce() bool`

True, if the CLI flag `-once` has been defined

```
print(runtime.isOnce())
```

#### `withScript() string`

The value of the CLI flag `-script <VALUE>`

```
print(runtime.withScript())
```

#### `configSource() string`

The value of the CLI flag `-config <VALUE>`

```
print(runtime.configSource())
```

