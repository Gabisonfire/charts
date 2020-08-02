# Wekan

## Open Source and Free software collaborative kanban board application

[Wekan](https://wekan.github.io/) is an completely Open Source and Free software collaborative kanban board application with MIT license.

## QuickStart

```bash
$ helm repo add gabisonfire https://gabisonfire.github.io/charts/
$ helm repo update
$ helm install foo gabisonfire/wekan --namespace bar
```

## Introduction

This chart deploys Wekan

## Prerequisites

- Kubernetes 1.4+
- Mongodb database

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install my-release gabisonfire/wekan --namespace bar
```

> **Tip**: List all releases using `helm list`

In order to deploy this chart under Kubernetes 1.9+, the `kubeMeta.deploymentApiVersion` MUST be set to "apps/v1".

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The configurable parameters of the Wekan chart and
their descriptions can be seen in `values.yaml`. The [full compose file](https://github.com/wekan/wekan/blob/master/docker-compose.yml) contains more information about Environments variables you can set in docker.

> **Tip**: You can use the default [values.yaml](values.yaml)

Here are the most common:

|             Parameter               |            Description              |                    Default                |
|-------------------------------------|-------------------------------------|-------------------------------------------|
| `replicaCount`                      | Number of replicas                  | `1`                                       |
| `image.repository`                  | The image to run                    | `wekanteam/wekan`                         |
| `image.tag`                         | The image tag to pull               | `v4.22`                                   |
| `image.pullPolicy`                  | Image pull policy                   | `IfNotPresent`                            |
| `image.pullSecrets`                 | Specify image pull secrets          | `nil`                                     |
| `service.type`                      | Type of Service                     | `ClusterIP`                               |
| `service.port`                      | Port for kubernetes service         | `80`                                      |
| `ingress.enabled`                   | Enable ingress                      | `false`                                   |
| `ingress.annotations`               | Annotations for ingress             | `{}`                                      |
| `ingress.hosts[0].host`             | Ingress host                        | `"chart-example.local"`                   |
| `ingress.hosts[0].paths`            | Ingress paths                       | `[]`                                      |
| `ingress.tls`                       | Ingress tls settings                | `[]`                                      |
| `resources`                         | Kubernetes ressources options       | `{}`                                      |
| `podSecurityContext`                | Pod security context settings       | `{}`                                      |
| `securityContext`                   | Security context settings           | `{}`                                      |
| `podAnnotations`                    | Pod annotations                     | `[]`                                      |
| `nodeSelector`                      | Node selector                       | `{}`                                      |
| `tolerations`                       | Tolerations                         | `[]`                                      |
| `affinity`                          | Affinity                            | `{}`                                      |
| `wekan.env.MONGO_URL`               | URL to the MongoDB host             | `mongodb://wekandb:27017/wekan`           |
| `wekan.env.ROOT_URL`                | URL to your Wekan instance          | `http://localhost`                        |