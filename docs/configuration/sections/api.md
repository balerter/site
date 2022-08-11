=== "HCL"
    ```tf
    api {
      address = "127.0.0.1:2000"
      serviceAddress = "127.0.0.1:2001"
      coreApi {
        address = "127.0.0.1:2200"
        authToken = "xxx"
      }
    }
    ```
=== "YAML"
    ```yaml
    api:
      address: 127.0.0.1:2000
      serviceAddress: 127.0.0.1:2001
      coreApi:
        address: 127.0.0.1:2200
        authToken: xxx
    ```

### address

> By default: empty (disabled)

If defined, API handler will be run on this address

### serviceAddress

> By default: empty (disabled)

If `serviceAddress` is defined, balerter will be listening this address.

- `/metrics` route for prometheus metrics (see more about [metrics](../api/metrics))
- `/` and `/liveness` you can use for liveness checks. It always returns `ok` with `200` status code

Also `pprof` routes will be run on this address:

- /debug/pprof/profile
- /debug/pprof/trace
- /debug/pprof/heap
- /debug/pprof/goroutine
- /debug/pprof/allocs

### coreApi

If Core API address is defined, balerter will run Core API server on this address.
If authToken is defined, it will be used for authentication.

Read more about [Core API](/core-api/about)