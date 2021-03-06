# goofys CSI driver for Kubernetes
[![Coverage Status](https://coveralls.io/github/csi-driver/goofys-csi-driver?branch=master)](https://coveralls.io/github/csi-driver/goofys-csi-driver?branch=master)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fcsi-driver%2Fgoofys-csi-driver.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fcsi-driver%2Fgoofys-csi-driver?ref=badge_shield)

### About
This driver allows Kubernetes to use [goofys](https://github.com/kahing/goofys), csi plugin name: `goofys.csi.azure.com`

### Container Images & CSI Compatibility:
|goofys CSI Driver Version    | Image                               | v1.0.0 |
|-----------------------------|------------------------------------ |--------|
|master branch                |andyzhangx/goofys-csi:latest       | yes    |

### Kubernetes Compatibility
| goofys CSI Driver\Kubernetes Version   | 1.14+ |
|----------------------------------------|-------|
| master branch                          | yes   |

### Driver parameters
Please refer to `goofys.csi.azure.com` [driver parameters](./docs/driver-parameters.md)
 > storage class `goofys.csi.azure.com` parameters are compatible with built-in [goofys](https://kubernetes.io/docs/concepts/storage/volumes/#goofys) plugin

### Prerequisite
 - The driver initialization depends on a [Cloud provider config file](https://github.com/kubernetes/cloud-provider-azure/blob/master/docs/cloud-provider-config.md), usually it's `/etc/kubernetes/azure.json` on all kubernetes nodes deployed by AKS or aks-engine, here is an [azure.json example](./deploy/example/azure.json)
 > if cluster is based on Managed Service Identity(MSI), make sure all agent nodes have `Contributor` role for current resource group

### Install goofys CSI driver on a kubernetes cluster
Please refer to [install goofys csi driver](https://github.com/csi-driver/goofys-csi-driver/blob/master/docs/install-goofys-csi-driver.md)

### Examples
 - [Basic usage](./deploy/example/e2e_usage.md)

## Kubernetes Development
Please refer to [development guide](./docs/csi-dev.md)


### Links
 - [goofys](https://github.com/kahing/goofys)
 - [Kubernetes CSI Documentation](https://kubernetes-csi.github.io/docs/Home.html)
 - [Analysis of the CSI Spec](https://blog.thecodeteam.com/2017/11/03/analysis-csi-spec/)
 - [CSI Drivers](https://github.com/kubernetes-csi/drivers)
 - [Container Storage Interface (CSI) Specification](https://github.com/container-storage-interface/spec)
