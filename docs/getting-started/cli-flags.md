```
-config=/path/to/config.yml         
 path to config file (yml or hcl)
 default: config.yml

-logLevel=[LOG LEVEL]
 log level. ERROR, INFO or DEBUG
 default: INFO

-debug
 turn on debug mode for logging in human-readable format
 default: false

-once
 once run scripts and exit
 default: false

-script=postgres.pg1.demoscript
 run only provided script

-json
 output json format (for balerter/test utility)

-safemode
 disable http module and embedded lua modules
```