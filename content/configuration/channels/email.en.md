---
title: "Email"
date: 2020-02-04T16:50:16+03:00
draft: false
weight: 5
---

Send Email 

```
email:
  - name: default
    from: foo@bar.com
    to: alert@bar.com
    cc: alert-cc@bar.com
    host: bar.com
    port: 1234
    username: user
    password: secret
    secure: ssl
    timeout: 1000
```

### name 

> Required, Unique

Channel name

### from

Field 'from'

### to

Field 'to'

### cc

Field 'cc'

### host

Hostname

### port

Port

If `Port` equals to '465' and `Secure` field is empty, `Secure` filed will be set to 'ssl'

### username

Username

### password

Password

### secure

`none`, `ssl`, `tls` or empty string

### timeout

timeout in seconds. By default - 10 sec.