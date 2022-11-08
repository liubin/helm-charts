# Nydus-snapshotter Helm Chart

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/dragonfly)](https://artifacthub.io/packages/search?repo=dragonfly)

## TL;DR

```shell
helm repo add dragonfly https://dragonflyoss.github.io/helm-charts/
helm install --create-namespace --namespace nydus-snapshotter nydus-snapshotter dragonfly/nydus-snapshotter
```

## Introduction

Nydus snapshotter is an external plugin of containerd for [Nydus image service](https://nydus.dev) which implements a chunk-based content-addressable filesystem on top of a called `RAFS (Registry Acceleration File System)` format that improves the current OCI image specification, in terms of container launching speed, image space, and network bandwidth efficiency, as well as data integrity with several runtime backends: FUSE, virtiofs and in-kernel [EROFS](https://www.kernel.org/doc/html/latest/filesystems/erofs.html).

Nydus supports lazy pulling feature since pulling image is one of the time-consuming steps in the container lifecycle. Lazy pulling here means a container can run even the image is partially available and necessary chunks of the image are fetched on-demand. Apart from that, Nydus also supports [(e)Stargz](https://github.com/containerd/stargz-snapshotter) lazy pulling directly **WITHOUT** any explicit conversion.

For more details about how to build Nydus container image, please refer to [nydusify](https://github.com/dragonflyoss/image-service/blob/master/docs/nydusify.md) conversion tool and [acceld](https://github.com/goharbor/acceleration-service).

## Prerequisites

- Kubernetes cluster 1.20+
- Helm v3.8.0+

## Installation Guide

For more detail about installation is available in [nydus-snapshotter repo](https://github.com/containerd/nydus-snapshotter).

## Installation

### Install with custom configuration

Create the `values.yaml` configuration file.

```yaml
nydussnapshotter:
  name: nydus-snapshotter
  image: ghcr.io/containerd/nydus-snapshotter/nydus-snapshotter
  tag: v1.2.11
```
Install nydus-snapshotter chart with release name `nydus-snapshotter`:

```shell
helm repo add dragonfly https://dragonflyoss.github.io/helm-charts/
helm install --create-namespace --namespace nydus-snapshotter nydus-snapshotter dragonfly/nydus-snapshotter -f values.yaml
```

## Uninstall

Uninstall the `dragonfly` deployment:

```shell
helm delete dragonfly --namespace dragonfly-system
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| fullnameOverride | string | `""` | Override nydus-snapshotter fullname |
| nameOverride | string | `""` | Override nydus-snapshotter name |
| nydussnapshotter.daemonsetAnnotations | object | `{}` | Daemonset annotations |
| nydussnapshotter.fullnameOverride | string | `""` | Override nydus-snapshotter fullname |
| nydussnapshotter.hostAliases | list | `[]` | Host Aliases |
| nydussnapshotter.hostNetwork | bool | `true` | Let nydus-snapshotter run in host network |
| nydussnapshotter.image | string | `"ghcr.io/liubin/nydus-snapshotter"` | Image repository image: ghcr.io/containerd/nydus-snapshotter/nydus-snapshotter |
| nydussnapshotter.name | string | `"nydus-snapshotter"` | nydus-snapshotter name |
| nydussnapshotter.nameOverride | string | `""` | Override nydus-snapshotter name |
| nydussnapshotter.nodeSelector | object | `{}` | Node labels for pod assignment |
| nydussnapshotter.podAnnotations | object | `{}` | Pod annotations |
| nydussnapshotter.podLabels | object | `{}` | Pod labels |
| nydussnapshotter.priorityClassName | string | `""` | Pod priorityClassName |
| nydussnapshotter.pullPolicy | string | `"Always"` | Image pull policy |
| nydussnapshotter.resources | object | `{"limits":{"cpu":"2","memory":"2Gi"},"requests":{"cpu":"0","memory":"0"}}` | Pod resource requests and limits |
| nydussnapshotter.tag | string | `"v1.2.11"` | Image tag |
| nydussnapshotter.terminationGracePeriodSeconds | string | `nil` | Pod terminationGracePeriodSeconds |
| nydussnapshotter.tolerations | list | `[]` | List of node taints to tolerate |

## Chart dependencies

| Repository | Name | Version |
|------------|------|---------|
