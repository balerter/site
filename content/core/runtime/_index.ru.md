---
title: "Runtime"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 10
---

Модуль `runtime` позволяет получить информацию о среде запуска

Использование:

```
local runtime = require('runtime')
```

### Методы

#### `logLevel() string`

Получение значения уровня лога (значение ключа командной строки `-logLevel <VALUE>`)

```
local logLevel = runtime.logLevel()
// INFO
```

#### `isDebug() bool`

True, если при запуске Balerter был установлен ключ командной строки `-debug`

```
print(runtime.isDebug())
```

#### `isOnce() bool`

True, если при запуске Balerter был установлен ключ командной строки `-once`

```
print(runtime.isOnce())
```

#### `withScript() string`

Значение ключа командной строки `-script <VALUE>`

```
print(runtime.withScript())
```

#### `configSource() string`

Путь к файлу конфигурации (Значение ключа командной строки `-config <VALUE>`)

```
print(runtime.configSource())
```

