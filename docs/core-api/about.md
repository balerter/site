Since `v0.10.0` Balerter provides Core API.

It's allows you to use core modules from your scripts, written and running outside Balerter with your preferred languages.

Libraries:

- [go](https://github.com/balerter/coreapi-go)
- [python](https://github.com/balerter/coreapi-python)

Feel for free for contributions for these or new libraries!

If you want to add new library for Balerter Core API, please check this [discussion](https://github.com/balerter/balerter/discussions/76)

For use Core API, you need to add `coreApi` section to your `api` configuration. [Read more](/configuration/sections/api)

## API

All API methods returns JSON response:

Success response:

```json
{
    "status": "ok",
    "result": <result data> 
}
```

Error response:

```json
{
    "status": "error",
    "error": "error message"
}
```