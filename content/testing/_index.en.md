+++
title = "Testing"
date = 2020-02-04T16:08:54+03:00
weight = 7
chapter = false
pre = "<b>VII. </b>"
+++

Balerter allows you write tests for your scripts!

For that you can use core module `test`. Run tests you can with `balerter/test` tool and same configuration file as main. 

Scrips will be obtain from scripts source, described in the configuration file. But all requests to datasources, or any core modules (as 'alert', 'kv' etc) will be mocked

### Writing tests

The main concept: One test script for one main script

An example:

Main script:
```
-- @name demoscript

log = require('log')

log.error('foo')
log.info('bar')
```


Now, write and discuss a test script:

```
-- @name demoscript-test
-- @test demoscript

test = requeire('test')

test.log().on('error', 'foo').response()
test.log().on('info', 'bar').response()

test.log().assertCalled('error', 'foo')
test.log().assertCalled('info', 'bar')
test.log().assertNotCalled('warn', 'baz')
```

With `@test` we did two things:
1. Defined that this file is a test.
2. Defined, that this test work with script with name 'demoscript'

### `test` module

> A module `test` can be included only in scripts, which marked as tests with a tag `@test`

You can:
- define data, which should be returned for calls to datasources or core modules in main script. If in the main script you wrote `log.error('foo')`, but in the test script you not define return value, you will get test error.
- define Asserts for calls, which you want or not

Module methods:
- `test.<MODULE>.on(<METHOD>, [<ARG>, <ARG>, ...]).response([<ARG>, <ARG>, ...])`
- `test.<MODULE>.assertCalled(<METHOD>, [<ARG>, <ARG>, ...])`
- `test.<MODULE>.assertNotCalled(<METHOD>, [<ARG>, <ARG>, ...])`

`<MODULE>` - it is may be `datasource(<DATASOURCE_NAME>)` for datasources. For example `test.datasource('postgres.prod')`. 

Or call core modules:
- log()
- http()
- chart()
- alert() 
- kv() 

For example:

```
-- define a response ('nil' at now) for call `log.error('error message')` in a main script
test.log().on('error', 'error message').response()

-- check, that we want to see call `alert.error('alert-id', 'alert message')`
test.alert().assertCalled('error', 'alert-id', 'alert message')

-- define response for a call ch1.query('SELECT * FROM users'), ch1 = require('datasource.clickhouse.ch1')
test.datasource('clickhouse.ch1').on('query', 'SELECT * FROM users').response({ { id = 1, name = 'John' } })
```

> Important! Even you call returns nothing (`log.info(...)`), you should register this call with `test.log().on('info', 'message').resoponse()`

### Run tests

You can use tool `test`

Docker image example:

```
docker run --rm \
    -v /path/to/config.yml:/opt/config.yml \
    -v /path/to/scripts:/opt/scripts \
    balerter/test -config=/opt/config.yml
```

If run fails, exit code will be equal 1. If run was success, but tests fails, exit code will be equals 2.  

An output example:
```
[FAIL]  [demo-test]     [alert] method 'success' with args [alert-id,All OK] was called, but should not
[PASS]  [demo-test]     [alert] method 'error' with args [alert-id Error get key] was not called
[PASS]  [demo-test]     [kv]    method 'get' with args [foo] was called
[FAIL]  [demo-test]     [result]        FAIL
```

First column - line result. Second column - a test script name. Third - a module name. Last - a message.
If you see `result` in Module name, that mean total result for the script 

Scripts from the example above:
```
-- main script
-- @name demo

alert = require('alert')
kv = require('kv')

v, err = kv.get('foo')

if err ~= nil then
    alert.error('alert-id', 'Error get key')
else
    alert.success('alert-id', 'All OK')
end
```

```
-- test script
-- @test demo
-- @name demo-test

test = require('test')

test.kv().on('get', 'foo').response(42, nil)
test.kv().assertCalled('get', 'foo')

test.alert().on('success', 'alert-id', 'All OK').response()
test.alert().assertNotCalled('success', 'alert-id', 'All OK')
test.alert().assertNotCalled('error', 'alert-id', 'Error get key')
```

### Plans

#### Ability to define `test.AnyValue` for Asserts or on...response

For example, registration response for the call `log.error(<ЛЮБОЕ ЗНАЧЕНИЕ>)`
```
test.log().on('error', test.AnyValue).response()
```

#### Ability to grouping tests for several isolated runs

Test script example:
```
test = require('test')

test.group('group name 1', function(t)
    t.log().on('error', 'message').response()
    t.alert().assertCalled('error', 'alert-id', 'message') 
end)

test.group('group name 2', function(t)
    t.group('group name 2-1', function(t2)
        t2.log().on('error', 'message').response()
        t2.alert().assertCalled('error', 'alert-id', 'message') 
    end)

    t.group('group name 2-2', function(t2)
        t2.log().on('error', 'message').response()
        t2.alert().assertCalled('error', 'alert-id', 'message') 
    end)
end)
```


> Vote for issues on the [github](https://github.com/balerter/balerter) or create new issues!
