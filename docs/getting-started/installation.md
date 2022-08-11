## Docker

The official images:

- [https://hub.docker.com/r/balerter](https://hub.docker.com/r/balerter)
- [https://github.com/orgs/balerter/packages](https://github.com/orgs/balerter/packages)

```bash
docker run \
    -v /path/to/config.yml:/opt/config.yml \
    balerter/balerter -config=/opt/config.yml
```

or

```bash
docker run \
    -v /path/to/config.yml:/opt/config.yml \
    ghcr.io/balerter/balerter -config=/opt/config.yml
```

## Build from sources

Clone the repo and build the Balerter

> Require Go 1.18 or later

```bash
git clone https://github.com/balerter/balerter.git
cd balerter
go build -o balerter ./cmd/balerter
```