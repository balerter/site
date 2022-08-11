Since `v0.10.0` Balerter provides Core API.

It's allows you to use core modules from your scripts, written and running outside Balerter with your preferred languages.

Libraries:

- [go (todo)](https://domain.com)
- [python (todo)](https://domain.com)

Feel for free for contributions for these or new libraries!

If you want to add new library for Balerter Core API, please check this [discussion](https://github.com/balerter/balerter/discussions/76)

???+ warning
    todo: describe `coreapi` config and add instructions for using it

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