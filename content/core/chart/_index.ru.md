---
title: "Chart"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 3
---

Модуль `chart` позволяет вам создать изображение с графиком, которое вы можете затем загрузить в хранилище и прикрепить к уведомлению

Подключение:

```
local chart = require('chart')
```

### Методы

#### `render('<CHART_TITLE>', <CHART_OPTIONS>) binaryImageData, error`

Метод `render` формирует изображение на основе переданных данных и возвращает это изображение первым параметром

Если во время рендера произошла ошибка, она будет возвращена вторым параметром

### Chart Options

Структура `<CHART_OPTIONS>` описывает данные, на основе которых формируется график

```
{
    series = { <CHART_SERIES>, <CHART_SERIES>, ... } 
}
```

Поле `series` содержит массив Серий (или отдельных линий на общем графике), которые будут нанесены на график

#### Series

```
{
    color = '<COLOR>',
    line_color = '<COLOR>',
    point_color = '<COLOR>',
    data = { <POINT_VALUE>, <POINT_VALUE>, ... }
}
```

Поля `color`, `line_color`, `point_color` позволяют указать общий цвет, цвет линий или цвет точек соответственно.
Если указан только `color` - он будет применяться и к линиям и к точкам.
Если цвет не указан, будет применяться цвет по-умолчанию: черный. Формат этого поля описан ниже.

Поле `data` содержит массив данных для каждой точки графика.

Одна точка графика описывается следующей структурой:

```
{
    timestamp = <FLOAT>
    value = <FLOAT>
}
```

#### Color

Поле `color` (`color_line`, `color_point`) может содержать следующие варианты:

Одну из предустановленных констант:
- blue
- red
- black
- green
- yellow

Либо строку вида `#XXXXXX` для указания цвета в формате RGB или `#XXXXXXXX` для указания в формате RGBA

Например:
```
color = 'blue'
color = '#00FF00'
color = '#ABCD12FA'
```

### Примеры:

Установка данных вручную:
```
local chartOptions = {
    ['series'] = {
        {
            ['color'] = '#456789',
            ["data"] = {
                { ['timestamp'] = 12345646554, ['value'] = 95 },
                { ['timestamp'] = 12345646555, ['value'] = 94 },
                { ['timestamp'] = 12345646556, ['value'] = 97 },
                { ['timestamp'] = 12345646557, ['value'] = 93 }
            }
        },
        {
            ['color'] = 'red',
            ["data"] = {
                { ['timestamp'] = 12345646554, ['value'] = 85 },
                { ['timestamp'] = 12345646555, ['value'] = 84 },
                { ['timestamp'] = 12345646556, ['value'] = 87 },
                { ['timestamp'] = 12345646557, ['value'] = 83 }
            }
        }
    }
}

local img, err = chart.render('My Chart', chartOptions)

-- img будет содержать изображение, которое можно загрузить в хранилище
```

![Example 1](example1.png)

Получение данных из Prometheus (в котором есть данные из [NodeExporter](https://github.com/prometheus/node_exporter))
```
local rangeOptions = {
    ['start'] = r - 86400,
    ['end'] = r,
    ['step'] = '3600'
}

res1 = prom.range('rate(sum(node_cpu_seconds_total{mode!="idle",node="32"}[5m])) / rate(sum(node_cpu_seconds_total{node="32"}[5m]))', rangeOptions)
res2 = prom.range('rate(sum(node_cpu_seconds_total{mode!="idle",node="43"}[5m])) / rate(sum(node_cpu_seconds_total{node="43"}[5m]))', rangeOptions)

local chartOptions = {
    ['series'] = {
        {
            ['color'] = '#456789',
            ["data"] = res1[1].values,
        },
        {
            ['color'] = 'red',
            ['line_color'] = 'blue',
            ["data"] = res2[1].values,
        }
    }
}


local img, err = chart.render('CPU', chartOptions)

-- img будет содержать изображение, которое можно загрузить в хранилище
```

![Example 2](example2.png)
