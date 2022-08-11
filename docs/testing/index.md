Balerter allows you to write tests for your scripts!

For that you can use core module `test`. Run tests you can with `balerter/test` tool and same configuration file as
main.

Scrips will be obtained from scripts source, described in the configuration file. But all requests to datasources, or
any core modules (as 'alert', 'kv' etc) will be mocked

## writing tests

The main concept: One test script (with one or more test functions) for one main script

An example:

Main script:

```lua title="script.lua"
-- @name demoscript

log = require('log')

log.error('foo')
log.info('bar')
-- log.warn('baz')
```

Now, write and discuss a test script:

```lua title="script_test.lua"
-- @name demoscript-test
-- @test demoscript

local function my_test(test)
    test.log().on('error', 'foo').response()
    test.log().on('info', 'bar').response()

    test.log().assertCalled('error', 'foo')
    test.log().assertCalled('info', 'bar')
    test.log().assertNotCalled('warn', 'baz')
end

return {
    ['My Test'] = my_test,
}

```

With `@test` we did two things:

1. Defined that this file is a test.
2. Defined, that this test work with script with name 'demoscript'

You can to define multiply test functions. The test function has one parameter - `test` module.

At the end of the test script you must return a table with test names as keys and test functions as values

## `test` module

???+ info
    A module `test` can be used only in test functions in scripts, which marked as tests with a tag `@test`

You can:

- define data, which should be returned for calls to datasources or core modules in main script. If in the main script
  you wrote `log.error('foo')`, but in the test script you not define return value, you will get test error.
- define Asserts for calls, which you want or not

Module methods:

### on

`test.<MODULE>.on(<METHOD>, [<ARG>, <ARG>, ...]).response([<ARG>, <ARG>, ...])`

### assertCalled

`test.<MODULE>.assertCalled(<METHOD>, [<ARG>, <ARG>, ...])`

### assertNotCalled

`test.<MODULE>.assertNotCalled(<METHOD>, [<ARG>, <ARG>, ...])`

---

`<MODULE>` - it is may be `datasource(<DATASOURCE_NAME>)` for datasources. For
example `test.datasource('postgres.prod')`.

Or call core modules:

- log()
- http()
- chart()
- alert()
- kv()

For example:

```lua title="script.lua"
-- define a response ('nil' at now) for call `log.error('error message')` in a main script
test.log().on('error', 'error message').response()

-- check, that we want to see call `alert.error('alert-id', 'alert message')`
test.alert().assertCalled('error', 'alert-id', 'alert message')

-- define response for a call ch1.query('SELECT * FROM users'), ch1 = require('datasource.clickhouse.ch1')
test.datasource('clickhouse.ch1').on('query', 'SELECT * FROM users').response({ { id = 1, name = 'John' } })
```

> Important! Even you call returns nothing (`log.info(...)`), you should register this call with `test.log().on('info', 'message').response()`

## run tests

You can use the tool `test`

Docker image example:

```bash
docker run --rm \
    -v /path/to/config.hcl:/opt/config.hcl \
    -v /path/to/scripts:/opt/scripts \
    balerter/test -config=/opt/config.hcl
```

If run fails, exit code will be equal 1. If run was success, but tests fails, exit code will be equals 2.

An output example:

```
[PASS]  [demo-test]     [test name 1]   [alert] method 'success' with args [alert-id,All OK] was called
[PASS]  [demo-test]     [test name 1]   [kv]    method 'get' with args [foo] was called
[PASS]  [demo-test]     [test name 1]   PASS
[FAIL]  [demo-test]     [test name 2]   [alert] method 'success' with args [alert-id,All OK] was called, but should not
[PASS]  [demo-test]     [test name 2]   [alert] method 'error' with args [alert-id Error get key] was not called
[PASS]  [demo-test]     [test name 2]   [kv]    method 'get' with args [foo] was called
[FAIL]  [demo-test]     [test name 2]   FAIL
[FAIL]  [demo-test]     FAIL
```

First column - line result. Second column - a test script name. Third - test function name. Fourth - a module name. Last - a message. 
Last line mean total result for the script

Scripts from the example above:

```lua title="script.lua"
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

```lua title="script_test.lua"
-- test script
-- @test demo
-- @name demo-test

local function test1(test)
    test.alert().on('success', 'alert-id', 'All OK').response()
    test.alert().assertCalled('success', 'alert-id', 'All OK')

    test.kv().on('get', 'foo').response(42, nil)
    test.kv().assertCalled('get', 'foo')
end

local function test2(test)
    test.alert().on('success', 'alert-id', 'All OK').response()
    test.alert().assertNotCalled('success', 'alert-id', 'All OK')
    test.alert().assertNotCalled('error', 'alert-id', 'Error get key')

    test.kv().on('get', 'foo').response(42, nil)
    test.kv().assertCalled('get', 'foo')
end

return {
    ['test name 1'] = test1,
    ['test name 2'] = test2,
}
```
