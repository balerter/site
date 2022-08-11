??? success "Core API"
    This module available in Core API

You can use this module for getting the information about domain certificates info 

## Usage:

```lua title="script.lua"
local tls = require('tls')
```

## Methods

### get 

`get() table, error`

Returns the certificate's info, and an error if occurred 

An example:

```lua title="script.lua"
local tls = require('tls')
local h = require('h')


local info = tls.get('google.com')
h.print(info)
```

```
{
    1 = {
        issuer = CN=GTS CA 1O1,O=Google Trust Services,C=US
        expiry = 1629077759
        dns names = *.google.com,*.appengine.google.com,*.bdn.dev,*.cloud.google.com,(...skipped)
        email addressed = 
    }
    2 = {
        issuer = CN=GlobalSign,OU=GlobalSign Root CA - R2,O=GlobalSign
        expiry = 1639526442
        dns names = 
        email addressed = 
    }
}
```
