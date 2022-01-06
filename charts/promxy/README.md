# promxy

promxy

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``sops``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

## How to install

Add repo:

```console
helm repo add 1mr https://charts.1mr.me
helm repo update
```

Test the installation with command:

```console
helm -n NAMESAPCE install promxy 1mr/promxy -f values.yaml --debug --dry-run
```

Install chart with command:

```console
helm -n NAMESAPCE install promxy 1mr/promxy -f values.yaml
```

## How to uninstall

Remove application with command.

```console
helm -n NAMESAPCE uninstall promxy -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs``.

Generate docs with ``helm-docs`` command.

```bash
cd charts/promxy

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``values.yaml`` file.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| config.global.evaluation_interval | string | `"5s"` |  |
| config.global.external_labels.source | string | `"promxy"` |  |
| config.promxy.server_groups[0].anti_affinity | string | `"10s"` |  |
| config.promxy.server_groups[0].http_client.dial_timeout | string | `"1s"` |  |
| config.promxy.server_groups[0].http_client.tls_config.insecure_skip_verify | bool | `true` |  |
| config.promxy.server_groups[0].path_prefix | string | `"/select/0/prometheus/"` |  |
| config.promxy.server_groups[0].query_params.nocache | int | `1` |  |
| config.promxy.server_groups[0].scheme | string | `"http"` |  |
| config.promxy.server_groups[0].static_configs[0].targets[0] | string | `"vmselect-az-b.victoria-metrics.svc.cluster.local:8481"` |  |
| config.promxy.server_groups[0].static_configs[0].targets[1] | string | `"vmselect-az-d.victoria-metrics.svc.cluster.local:8481"` |  |
| extra_args.log-level | string | `"info"` |  |
| image.repository | string | `"quay.io/jacksontj/promxy"` |  |
| image.tag | string | `"v0.0.75"` |  |
| livenessProbe | object | `{}` |  |
| podSecurityContext.allowPrivilegeEscalation | bool | `false` |  |
| podSecurityContext.capabilities.drop[0] | string | `"all"` |  |
| podSecurityContext.runAsNonRoot | bool | `true` |  |
| readinessProbe | object | `{}` |  |
| replicaCount | int | `2` |  |
| resources.limits.cpu | string | `"200m"` |  |
| resources.limits.memory | string | `"100Mi"` |  |
| resources.requests.cpu | string | `"50m"` |  |
| resources.requests.memory | string | `"50Mi"` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| service.enabled | bool | `true` |  |
| serviceAccount.create | bool | `true` |  |
