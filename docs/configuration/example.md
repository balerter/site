Config file example

=== "HCL"
    ```tf title="config.hcl"
    scripts {
      updateInterval = 5000
      folder "scripts"{
        path = "/opt/scripts"
        mask = "*.lua" 
      }
      file "demo1" {
        filename = "/path/to/demo.lua"
      }
    }
    
    datasources {
      clickhouse "ch1" {
        host = "domain.com"
        port = 6440
        username = "username"
        password = "password"
        database = "database"
        sslCertPath = "/path/to/cert.crt"
        timeout = 3000 
      }
      prometheus "prom1" {
        url = "domain.com"
        timeout = 3000
        basicAuth {
          username = "username"
          password = "password"
        }
      }
      postgres "pg1" {
        host = "domain.com"
        port = 5432
        username = "username"
        password = "password"
        database = "database"
        sslMode = "verify-full"
        sslCertPath = "/path/to/cert.crt"
        timeout = 3000
      }
      mysql "mysql1" {
        dsn = "user:secret@tcp(127.0.0.1:3306)/database"
        timeout = 3000
      }
      loki "loki1" {
        url = "domain.com"
        timeout = 5000
        basicAuth {
          username = "username"
          password = "password"
        }
      }
    }
    
    
    channels {
      slack "slack-notification" {
        token = "SLACK-APPLICATION-TOKEN"
        channel = "notification"
        ignore = false
      }
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
      syslog "default" {
        tag = "balerter"
        network = "tcp"
        address = "127.0.0.1:10515"
        priority = "EMERG|DAEMON"
        ignore = false
      }
      notify "default" {
        icons {
          success = "/path/to/logo-success.png"
          error = "/path/to/logo-error.png"
          warning = "/path/to/logo-warning.png"
        }
        ignore = false
      }
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
      discord "default" {
        token = "ABCD"
        channelId = 1234
        ignore = false
      }
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
            body = "body content"
          }
          timeout = 5000
          headers {
            X-Foo = "Bar"
          }
        }
        ignore = false
      }
      
      alertmanager "am1" {
        settings {
          // webhook settings
        }
        ignore = false
      }
    
      alertmanager_receiver "am2" {
        settings {
          // webhook settings
        }
        ignore = false
      }
      
      twilioVoice "tw1" {
        sid = "ABCD"
        token = "ABCD"
        from = "+11111111111"
        to = "+11111111111"
        twiml = "<Response><Say>{TEXT}</Say></Response>"
        ignore = false
        timeout = 5000
      }
    }
    
    storagesCore {
      sqlite "mySqliteStorage" {
        path = "/path/to/file"
        timeout = 1000
        tableKV {
          table = "kv"
          fields {
            key = "key"
            value = "value"
          }
        }
        tableAlerts {
          table = "alerts"
          fields {
            name = "id"
            level = "level"
            count = "count"
            createdAt = "created_at"
            updatedAt = "updated_at"
          }
        }
      }
      
      postgres "pg1" {
        host = "domain.com"
        port = 5432
        username = "username"
        password = "password"
        database = "database"
        sslMode = "verify-full"
        sslCertPath = "/path/to/cert.crt"
        timeout = 3000
        tableKV = {} // same as sqlite above
        tableAlerts = {} // same as sqlite above
      }
    }
    
    storagesUpload {
      s3 "dev" {
        region = "us-east1"
        key = "SOME_KEY"
        secret = "SOME_SECRET"
        endpoint = "SOME_ENDPOINT"
        bucket = "SOME_BUCKET" 
      }
    }
    
    api {
      address = "127.0.0.1:2000"
      serviceAddress = "127.0.0.1:2001"
    }
    
    storageAlert = "memory"
    storageKV = "sqlite.mySqliteStorage"
    luaModulesPath = "./?.lua;./modules/?.lua;./modules/?/init.lua;/modules/?.lua;/modules/?/init.lua"
    
    system {
      jobWorkersCount = 32
      cronLocation = 'UTC'
    }
    ```
=== "YAML"
    ```yaml title="config.yml"
    scripts:
      updateInterval: 5000
      folder:
        - name: scripts
          path: /opt/scripts
          mask: '*.lua'
      file:
        - name: demo1
          filename: /path/to/demo.lua
    
    datasources:
      clickhouse:
        - name: ch1
          host: domain.com
          port: 6440
          username: username
          password: password
          database: database
          sslCertPath: /path/to/cert.crt
          timeout: 3000
    
      prometheus:
        - name: prom1
          url: domain.com
          timeout: 3000
          basicAuth:
            username: username
            password: password
    
      postgres:
        - name: pg1
          host: domain.com
          port: 5432
          username: username
          password: password
          database: database
          sslMode: verify-full
          sslCertPath: /path/to/cert.crt
          timeout: 3000
      
      mysql:
        - name: mysql1
          dsn: user:secret@tcp(127.0.0.1:3306)/database
          timeout: 3000
    
      loki:
        - name: loki1
          url: domain.com
          timeout: 5000
          basicAuth:
            username: username
            password: password
    
    channels:
      slack:
        - name: slack-notification
          token: SLACK-APPLICATION-TOKEN
          channel: notification
          ignore: false
    
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
      syslog:
        - name: default
          tag: balerter
          network: tcp
          address: 127.0.0.1:10515
          priority: 'EMERG|DAEMON'
          ignore: false
      
      notify:
        - name: default
          icons:
            success: /path/to/logo-success.png
            error: /path/to/logo-error.png
            warning: /path/to/logo-warning.png
          ignore: false
    
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
          timeout: 10
          ignore: false
    
      discord:
        - name: default
          token: 'ABCD'
          channelId: 1234
          ignore: false
    
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
              body: body content
            timeout: 5000
            headers:
              X-Foo: Bar
          ignore: false
    
      alertmanager:
        - name: am1
          settings: # webhook settings
          ignore: false
    
      alertmanager_receiver:
        - name: am2
          settings: # webhook settings
          ignore: false
    
      twilioVoice:
        - name: tw1
          sid: ABCD
          token: ABCD
          from: +11111111111
          to: +11111111111
          twiml: '<Response><Say>{TEXT}</Say></Response>'
          ignore: false
          timeout: 5000
    
    storagesCore:
      sqlite:
        - name: mySqliteStorage
          path: /path/to/file
          timeout: 1000
          tableKV:
            table: "kv"
            fields:
              key: key
              value: value
          tableAlerts:
            table: "alerts"
            fields:
              name: id
              level: level
              count: count
              createdAt: created_at
              updatedAt: updated_at
      postgres:
        - name: pg1
          host: domain.com
          port: 5432
          username: username
          password: password
          database: database
          sslMode: verify-full
          sslCertPath: /path/to/cert.crt
          timeout: 3000
          tableKV: # same as sqlite above
          tableAlerts: # same as sqlite above
    
    storagesUpload:
      s3:
        - name: dev
          region: us-east1
          key: SOME_KEY
          secret: SOME_SECRET
          endpoint: SOME_ENDPOINT
          bucket: SOME_BUCKET
    
    api:
      address: 127.0.0.1:2000
      serviceAddress: 127.0.0.1:2001
    
    storageAlert: memory
    storageKV: sqlite.mySqliteStorage
    luaModulesPath: ./?.lua;./modules/?.lua;./modules/?/init.lua;/modules/?.lua;/modules/?/init.lua
    
    system:
      jobWorkersCount: 32
      cronLocation: 'UTC'
    ```


