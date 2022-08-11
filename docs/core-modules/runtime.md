??? success "Core API"
    This module available in Core API

Module `runtime` allows you to get an information about the Balerter runtime

Usage:

```lua title="script.lua"
local runtime = require('runtime')
```

## Methods

### logLevel 

`logLevel() string`

Get a logger level value (CLI flag `-logLevel <VALUE>`)

```lua title="script.lua"
local logLevel = runtime.logLevel()
// INFO
```

### isDebug 

`isDebug() bool`

True, if the CLI flag `--debug` has been defined

```lua title="script.lua"
print(runtime.isDebug())
```

### isOnce 

`isOnce() bool`

True, if the CLI flag `--once` has been defined

```lua title="script.lua"
print(runtime.isOnce())
```

### withScript 

`withScript() string`

The value of the CLI flag `-script <VALUE>`

```lua title="script.lua"
print(runtime.withScript())
```

### configSource 

`configSource() string`

The value of the CLI flag `-config <VALUE>`

```lua title="script.lua"
print(runtime.configSource())
```

### safeMode 

`safeMode() bool`

The value of the CLI flag `--safemode`

```lua title="script.lua"
print(runtime.safeMode())
```

