# Wekan

## Open Source and Free software collaborative kanban board application

[Wekan](https://wekan.github.io/) is an completely Open Source and Free software collaborative kanban board application with MIT license.

## QuickStart

```bash
$ helm install . foo --namespace bar
```

## Introduction

This chart deploys Wekan

## Prerequisites

- Kubernetes 1.4+
- Mongodb database

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install . my-release --namespace mynamespace
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