# Secrets

You can use secrets in your configuration file.

Supported secret engines:

- env
- vault

## Format

```
{secret:<ENGINE>:<KEY>}
```

For the `env` engine `key` is the environment variable name

For the `vault` engine `key` should look as `path/to/secret@field_name`

You can use env variables for vault connection

- `BALERTER_VAULT_URL`
- `BALERTER_VAULT_TOKEN`
- `BALERTER_VAULT_NAMESPACE` (optional)

## An example

=== "HCL"
    ```tf
    channels {
      telegram "tg1" {
        token = "{secret:env:TELEGRAM_TOKEN}"
        chatId = 100500
      }
    
      telegram "tg2" {
        token = "{secret:vault:secret/data/telegram@token}"
        chatId = 100500
      }
    }
    ```
=== "YAML"
    ```yaml
    channels:
        telegram:
            - name: tg1
              token: "{secret:env:TELEGRAM_TOKEN}"
              chatId: 100500

            - name: tg2
              token: "{secret:vault:secret/data/telegram@token}"
              chatId: 100500
    ```
