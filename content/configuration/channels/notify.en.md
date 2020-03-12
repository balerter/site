---
title: "Notify"
date: 2020-02-04T16:50:16+03:00
draft: false
weight: 4
---

Send standard OS GUI notification 

```
notify:
  - name: default
    icons:
      success: /path/to/logo-success.png
      error: /path/to/logo-error.png
      warning: /path/to/logo-warning.png
```

### name 

> Required, Unique

Channel name

### icons.success/error/warning

> By default: empty string

Path to images (use as notification icons)
