# Raneto

## Raneto is a free, open, simple Markdown powered knowledge base for Node.js.

[Raneto](http://raneto.com/) Raneto is a free, open, simple Markdown powered knowledge base for Node.js.

## QuickStart

```bash
$ helm repo add gabisonfire https://gabisonfire.github.io/charts/
$ helm repo update
$ helm install foo gabisonfire/raneto --namespace bar
```

## Introduction

This chart deploys Raneto based on https://hub.docker.com/r/linuxserver/raneto

## Prerequisites

- Kubernetes 1.14+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install my-release gabisonfire/raneto --namespace bar
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

The configurable parameters of the Raneto chart and
their descriptions can be seen in `values.yaml`.

> **Tip**: You can use the default [values.yaml](values.yaml)

Here are the most common:

|             Parameter               |            Description              |                    Default                |
|-------------------------------------|-------------------------------------|-------------------------------------------|
| `replicaCount`                      | Number of replicas                  | `1`                                       |
| `image.repository`                  | The image to run                    | `ghcr.io/linuxserver/raneto`              |
| `image.tag`                         | The image tag to pull               | `version-0.16.6`                          |
| `image.pullPolicy`                  | Image pull policy                   | `IfNotPresent`                            |
| `image.pullSecrets`                 | Specify image pull secrets          | `nil`                                     |
| `service.type`                      | Type of Service                     | `ClusterIP`                               |
| `service.port`                      | Port for kubernetes service         | `3000`                                    |
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
| `persistence.content.enabled`       | Persistence for Markdown files      | `true`                                    |
| `persistence.images.enabled`        | Persistence for image files         | `true`                                    |
| `gitsync.enabled`                   | Enable git repo syncing             | `false`                                   |
| `gitsync.repo`                      | Repository to synchronize           | `''`                                      |
| `gitsync.destination`               | Destination folder                  | `repo`                                    |
| `gitsync.every`                     | Sync every x seconds                | `600`                                     |
| `gitsync.authenticate`              | Use git authentication (see below)  | `false`                                   |
| `gitsync.ssh`                       | Use SSH for authentication          | `false`                                   |
| `raneto.site_title`                 | Site title                          | `Raneto`                                  |
| `raneto.authentication`             | Enable basic authentication         | `true`                                    |
| `raneto.authentication_for_edit`    | Enable authentication for editing   | `true`                                    |
| `raneto.authentication_for_read`    | Enable authentication for reading   | `false`                                   |
| `raneto.home_meta.title`            | Home title                          | `Custom Home Title`                       |
| `raneto.home_meta.description`      | Home Description                    | `Custom Home Description`                 |
| `raneto.table_of_contents`          | Enable table of content             | `false`                                   |

## Gitsync

Setting `gitsync.enabled` to `true` will sync `gitsync.repo` to `gitsync.destination` relative to `/content/` which is the folder containing your markdown files. The sync will occur at start and then every x seconds defined by `gitsync.every`.

### Authentication

If you need to use authenticated git repo, you will need to set `gitsync.authenticate` to `true` and then either provide a secret name to `gitsync.password.secret`.

Here's an example:
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: raneto-gitsync
type: Opaque
data:
  password: eW91IHJlYWxseSB0b29rIHRoZSB0aW1lIHRvIGRlY29kZSB0aGlzPw==
```

For ssh authentication, you'll need to set `gitsync.ssh` to `true`. Then you will have to specify a secret containing your ssh key `gitsync.ssh_secret`
You can create a secret using:
```
kubectl create secret generic raneto-gitsync-ssh --from-file=ssh=/path/to/.ssh/id_rsa
```