Upload storage use for uploading any data from your scripts (usually chart images)

At the moment supports only AWS S3 compatible storage

=== "HCL"
    ```tf
    storagesUpload {
      s3 "dev" {
        region = "us-east1"
        key = "SOME_KEY"
        secret = "SOME_SECRET"
        endpoint = "SOME_ENDPOINT"
        bucket = "SOME_BUCKET"
      }
    }
    ```
=== "YAML"
    ```yaml
    storagesUpload:
      s3:
        - name: dev
          region: us-east1
          key: SOME_KEY
          secret: SOME_SECRET
          endpoint: SOME_ENDPOINT
          bucket: SOME_BUCKET
    ```

For example:

```lua title="script.lua"
local storage = require('storage.s3.myUploadStorage')

imageURL, err = storage.uploadPNG(binaryData)
```

