# Installation with Helm

Quick start instructions for the setup and configuration of goofys CSI driver using Helm.

## Prerequisites

1. [install Helm Client](https://helm.sh/docs/using_helm/#installing-the-helm-client)

2. [initialize Helm and install Tiller](https://helm.sh/docs/using_helm/#initialize-helm-and-install-tiller)

## Install BlobFuse via `helm install`

```console
$ cd $GOPATH/src/sigs.k8s.io/goofys-csi-driver/charts/latest
$ helm package goofys-csi-driver
$ helm install goofys-csi-driver goofys-csi-driver-latest.tgz --namespace kube-system
```

## Uninstall

```console
$ helm delete --purge goofys-csi-driver
```
