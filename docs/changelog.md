## v0.10.0 (2022-08-12)

- add [Core API](/core-api)
- add colors marks to slack messages

## v0.9.4 (2022-05-26)

- cli flag `--safemode` for disable the `http` core module and `os` and `io` lua modules

## v0.9.3 (2022-04-19)

- Support for escalate alerts with `@escalate` meta-tag 

## v0.9.2 (2022-03-10)

- add core module 'file' [See more](/core-modules/file)
- refactoring telegram channel api. It's possible to send image directly from `chart.render`, without store to the S3 storage
- remove escaping special characters for telegram messages

## v0.9.1 (2021-12-19)

- use pgxpool for postgres connections
- add missed 'resend' alert options behavior
- add options for http.request
  - insecureSkipVerify
  - timeout

## v0.9.0 (2021-10-07)

- update testing subsystem. Use test functions. [See more](/testing)

## v0.8.4 (2021-09-23)

- Add alert option fields

## v0.8.3 (2021-09-23)

- add meta module [read more](/core-modules/meta)
- add config option system.cronLocation [read more](/configuration/system)

## v0.8.2 (2021-08-30)

- secrets in the config file, [read more](/configuration/secrets)

## v0.8.1 (2021-07-09)

- add config block `system`
- support for multiple job workers (Eliminates freezes during long execution of one script)

## v0.8.0 (2021-07-08)

- add the `Twilio Voice` channel, see a [configuration](/configuration/channel)
- add option `Ignore` to all channels
- add the `resend` alias for the `repeat` field for the alert options (scripts)

## v0.7.3 (2021-06-17)

- add the `tls` core module. getting the information about domain certificates

## v0.7.2 (2021-04-09)

- add the prometheus metric for exposing alerts levels (see [documentation](/api/metrics))
    - `balerter_alert_status`
- use ubuntu 20.10 as base image for docker images

## v0.7.1 (2021-04-02)

- bugfix: use milliseconds for datasource configs
- add core module `api` for getting information about the request, if script was run with API call
- add API for run the script by name
- switch to go 1.16

## v0.7.0 (2021-03-05)

> Breaking changes

This release has many breaking changes in:
- configuration structure
- alerts/kv storages
- script sources
- use `@cron` instead `@interval` in scripts
- etc

Please see actual information on this site.


