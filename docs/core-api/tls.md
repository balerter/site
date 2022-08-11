This endpoint allows to use [tls](/core-modules/tls) core module

## methods

### get

Call `tls` module with `get` function

#### request

> `POST /tls/get`

- request body - domain

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/tls/get" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "domain.com"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local tls = require("tls")
result = tls.get('domain.com')
```

#### response

```json
{
  "status": "ok",
  "result": [
    {
      "issuer": "CN=Sectigo RSA Domain Validation Secure Server CA,O=Sectigo Limited,L=Salford,ST=Greater Manchester,C=GB",
      "expiry": 1662767999,
      "dns_names": [
        "*.domain.com",
        "domain.com"
      ],
      "email_addresses": null
    },
    {
      "issuer": "CN=USERTrust RSA Certification Authority,O=The USERTRUST Network,L=Jersey City,ST=New Jersey,C=US",
      "expiry": 1924991999,
      "dns_names": null,
      "email_addresses": null
    },
    {
      "issuer": "CN=AAA Certificate Services,O=Comodo CA Limited,L=Salford,ST=Greater Manchester,C=GB",
      "expiry": 1861919999,
      "dns_names": null,
      "email_addresses": null
    }
  ]
}
```

