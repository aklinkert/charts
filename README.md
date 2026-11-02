# charts

[![test](https://github.com/aklinkert/charts/actions/workflows/test.yml/badge.svg)](https://github.com/aklinkert/charts/actions/workflows/test.yml)

Helm charts, published to GitHub Pages with
[chart-releaser](https://github.com/helm/chart-releaser).

| Chart | Description |
| ----- | ----------- |
| [`secret`](secret) | Renders a Kubernetes Secret from plain-text values and base64-encodes them |

## Usage

```sh
helm repo add aklinkert https://aklinkert.github.io/charts
helm repo update
helm install my-secret aklinkert/secret --set data.password=s3cret
```

## Chart: secret

Creates one `Secret` named `<release>-secret` (or `fullnameOverride`). Values
under `data` are plain text; the chart base64-encodes them.

| Value | Default | Description |
| ----- | ------- | ----------- |
| `type` | `Opaque` | Secret type |
| `data` | `{}` | Map of key to plain-text value |
| `nameOverride` | `""` | Overrides the chart name part of the resource name |
| `fullnameOverride` | `""` | Overrides the full resource name |

```yaml
data:
  username: admin
  password: s3cret
```

Values passed this way end up in Helm release history; prefer an external
secret manager for sensitive data.

## Development

Pull requests run `helm lint` and `ct lint` and must bump the chart `version`
in `Chart.yaml`. Pushes to `main` publish every chart version that has no
release yet.
