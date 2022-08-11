Section `channels` describes the channels that are available for send notifications.  

Supported channels:

- [slack](#slack)
- [telegram](#telegram)
- [syslog](#syslog)
- [notify](#notify)
- [email](#email)
- [discord](#discord)
- [webhook](#webhook)
- [alertmanager](#alertmanager)
- [alertmanager receiver](#alertmanager-receiver)
- [twilio voice](#twilio-voice)

## Slack

=== "HCL"
      ```tf
      slack "slack-notification" {
        token = "SLACK-APPLICATION-TOKEN"
        channel = "notification"
        ignore = false
      }
      ```
=== "YAML"
      ```yaml
      slack:
        - name: slack-notification
          token: SLACK-APPLICATION-TOKEN
          channel: notification
      ```


### name

string

> Required, Unique

Channel name

### token

string

> Required

Slack application token

### channel

string

> Required

Slack channel

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---


## Telegram

=== "HCL"
    ```tf
    telegram "tg1" {
      token = "TELEGRAM-BOT-TOKEN"
      chatId = 100500
      timeout = 5000
      proxy {
        address = "10.20.30.40:5060"
        auth {
          username = "username"
          password = "password"
        }
      }
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    telegram:
      - name: tg1
        token: TELEGRAM-BOT-TOKEN
        chatId: 100500
        timeout: 5000
        proxy:
          address: 10.20.30.40:5060
          auth:
            username: user
            password: secret
        ignore: false
    ```

### name 

string

> Required, Unique

Channel name

### token

string

> Required

Telegram bot API token

### chatId 

int

> Required

Chat ID

### timeout 

int

> By default: 5000 (5 sec)

timeout in milliseconds

### proxy

Socks5 proxy settings

If `auth` section is defined, it will use for authentication

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## Syslog

JSON marshalled messaged will be send to syslog server

=== "HCL"
    ```tf
    syslog "default" {
      tag = "balerter"
      network = "tcp"
      address = "127.0.0.1:10515"
      priority = "EMERG|DAEMON"
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    syslog:
      - name: default
        tag: balerter
        network: tcp
        address: 127.0.0.1:10515
        priority: EMERG|DAEMON
        ignore: false
    ```

### name

string

> Required, Unique

Channel name

### tag

string

Syslog tag

### network

string

Network type
- `udp`
- `tcp`
- empty string for use local syslog server

### address

string

Server address

### priority

string

> Default: `EMERG`

Message priority

Format: `<SEVERITY>[|<FACILITI>]`

Severity:

- EMERG
- ALERT
- CRIT
- ERR
- WARNING
- NOTICE
- INFO
- DEBUG

Facility:

- KERN
- USER
- MAIL
- DAEMON
- AUTH
- SYSLOG
- LPR
- NEWS
- UUCP
- CRON
- AUTHPRIV
- FTP
- LOCAL0
- LOCAL1
- LOCAL2
- LOCAL3
- LOCAL4
- LOCAL5
- LOCAL6

For example:

```yaml
priority: 'ALERT'
priority: 'ALERT|USER'
priority: 'INFO|LOCAL0'
```

### ignore 

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

--- 

## Notify

Send standard OS GUI notification

=== "HCL"
    ```tf
    notify "default" {
      icons {
        success = "/path/to/logo-success.png"
        error = "/path/to/logo-error.png"
        warning = "/path/to/logo-warning.png"
      }
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    notify:
      - name: default
        icons:
          success: /path/to/logo-success.png
          error: /path/to/logo-error.png
          warning: /path/to/logo-warning.png
        ignore: false
    ```

### name

string

> Required, Unique

Channel name

### icons 

- success
- error
- warning
- 
string

Path to images (use as notification icons)

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## Email

=== "HCL"
    ```tf
    email "default" {
      from = "foo@bar.com"
      to = "alert@bar.com"
      cc = "alert-cc@bar.com"
      host = "bar.com"
      port = 1234
      username = "user"
      password = "secret"
      secure = "ssl"
      timeout = 10
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
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
        ignore: false
    ```

### name

string

> Required, Unique

Channel name

### from

string

Field 'from'

### to

string

Field 'to'

### cc

string

Field 'cc'

### host

string

Hostname

### port

int

Port

If `Port` equals to '465' and `Secure` field is empty, `Secure` filed will be set to 'ssl'

### username

string

Username

### password

string

Password

### secure

string

`none`, `ssl`, `tls` or empty string

### timeout

int

timeout in seconds. By default - 10 sec.

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## Discord

=== "HCL"
    ```tf
    discord "default" {
      token = "ABCD"
      channelId = 1234
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    discord:
      - name: default
        token: ABCD
        channelId: 1234
        ignore: false
    ```


### name

string

> Required, Unique

Channel name

### token

string

Token

### channelID

int

Channel ID

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## Webhook

=== "HCL"
    ```tf
    webhook "wh1" {
      settings {
        url = "http://domain.com"
        method = "POST"
        auth {
          type = "basic"
          login = "user"
          password = "secret"
        }
        payload {
          queryParams {
            foo = "bar"
          }
          body = "body $text content"
        }
        timeout = 5000
        headers {
          X-Foo = "Bar"
        }
      }
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    webhook:
      - name: wh1
        settings:
          url: http://domain.com
          method: POST
          auth:
            type: basic
            login: user
            password: secret
          payload:
            queryParams:
              foo: bar
            body: body $text content
          timeout: 5000
          headers:
            X-Foo: Bar
        ignore: false
    ```

When you provide text in `payload.body`, you can use macros:

- `$level` 
- `$alert_name` 
- `$text` 
- `$image` 
- `$fields` 

### name

string

> Required, Unique

### settings.url

> Required, URL

Webhook URL

### settings.method

> By default: POST

HTTP method

### settings.auth

> Type must be `none`, `basic`, `bearer` or `custom`. By default: `none` (empty string)

Authentication data. Depending on the type:

#### type: basic

Should be not empty:
- settings.auth.login
- settings.auth.password

#### type: bearer

Should be not empty:
- settings.auth.token

### settings.payload.body

POST body. Must be defined with method=POST

### settings.payload.queryParams

String=String pairs for set query params

### settings.timeout (time interval)

> By default: 3000

Timeout in milliseconds

### settings.headers

String=String pairs for set HTTP request headers

### ignore (bool)

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## Alertmanager

> TODO: links to 
> - alertmanager docs
> - manual for balerter-alertmanager communications

=== "HCL"
    ```tf
    alertmanager "am1" {
      settings {
        // webhook settings
      }
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    alertmanager:
      - name: am1
        settings: # webhook settings
        ignore: false
    ```

### name

string

> Required, Unique

### settings

See `webhook settings`

### ignore 

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## alertmanager receiver

> TODO: links to
> - alertmanager-receiver docs
> - manual for balerter-alertmanager_receiver communications

=== "HCL"
    ```tf
    alertmanager_receiver "am2" {
      settings {
        // webhook settings
      }
      ignore = false
    }
    ```
=== "YAML"
    ```yaml
    alertmanager_receiver:
      - name: am2
        settings: # webhook settings
        ignore: false
    ```

### name 

string

> Required, Unique

### settings

See `webhook settings`

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

---

## twilio voice

TwilioVoice channel allows you to make voice calls on change alert status

> https://www.twilio.com/

=== "HCL"
    ```tf
    twilioVoice "tw1" {
      sid = "ABCD"
      token = "ABCD"
      from = "+11111111111"
      to = "+11111111111"
      twiml = "<Response><Say>{TEXT}</Say></Response>"
      ignore = false
      timeout = 5000
    }
    ```
=== "YAML"
    ```yaml
    twilioVoice:
      - name: tw1
        sid: ABCD
        token: ABCD
        from: +11111111111
        to: +11111111111
        twiml: '<Response><Say>{TEXT}</Say></Response>'
        ignore: false
        timeout: 5000
    ```

### name

string

> Required, Unique

### sid

string

> Required

Your SID from the Twilio console

### token

string

Your Token from the Twilio console

### from

string

Sender phone number

### to

string

Your phone number

### twiml

string

TwiML template.

You can to specify the macros `{TEXT}`, which will be replaced to alert text.
If this option is empty, alert text will be placed as TwiML template

### ignore

bool

If this option is True, this channel will be ignored by default.
This option will be ignored if you explicitly define the channel in your script meta-tags or alert options

### timeout 

int

> Default: 30000 (30s)

HTTP request timeout, milliseconds