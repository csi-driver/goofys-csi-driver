## CSI driver E2E usage example
create a pod with goofys mount on linux
### Dynamic Provisioning (create storage account and container by goofys driver)
 - Create a goofys CSI storage class
```console
kubectl create -f https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/storageclass-goofys-csi.yaml
```

 - Create a goofys CSI PVC
```console
kubectl create -f https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/pvc-goofys-csi.yaml
```

### Static Provisioning(use an existing storage account)
#### Option#1: use existing credentials in k8s cluster
 > make sure the existing credentials in k8s cluster(e.g. service principal, msi) could access the specified storage account
 - Download a goofys CSI storage class, edit `resourceGroup`, `storageAccount`, `containerName` in storage class
```console
wget https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/storageclass-goofys-csi-existing-container.yaml
vi storageclass-goofys-csi-existing-container.yaml
kubectl create -f storageclass-goofys-csi-existing-container.yaml
```

 - Create a goofys CSI PVC
```console
kubectl create -f https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/pvc-goofys-csi.yaml
```

#### Option#2: provide storage account name and key(or sastoken)
 - Use `kubectl create secret` to create `azure-secret` with existing storage account name and key(or sastoken)
```console
kubectl create secret generic azure-secret --from-literal azurestorageaccountname=NAME --from-literal azurestorageaccountkey="KEY" --type=Opaque
#kubectl create secret generic azure-secret --from-literal azurestorageaccountname=NAME --from-literal azurestorageaccountsastoken
="sastoken" --type=Opaque
```

> storage account key(or sastoken) could also be stored in Azure Key Vault, check example here: [read-from-keyvault](../../docs/read-from-keyvault.md)

 - Create a goofys CSI PV, download `pv-goofys-csi.yaml` file and edit `containerName` in `volumeAttributes`
```console
wget https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/pv-goofys-csi.yaml
vi pv-goofys-csi.yaml
kubectl create -f pv-goofys-csi.yaml
```

 - Create a goofys CSI PVC which would be bound to the above PV
```console
kubectl create -f https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/pvc-goofys-csi-static.yaml
```

#### 2. Validate PVC status and create an nginx pod
 > make sure pvc is created and in `Bound` status
```console
watch kubectl describe pvc pvc-goofys
```

 - create a pod with goofys CSI PVC
```console
kubectl create -f https://raw.githubusercontent.com/csi-driver/goofys-csi-driver/master/deploy/example/nginx-pod-goofys.yaml
```

#### 3. enter the pod container to do validation
 - watch the status of pod until its Status changed from `Pending` to `Running` and then enter the pod container
```console
$ watch kubectl describe po nginx-goofys
$ kubectl exec -it nginx-goofys -- bash
Filesystem      Size  Used Avail Use% Mounted on
...
goofys         30G  8.9G   21G  31% /mnt/goofys
/dev/sda1        30G  8.9G   21G  31% /etc/hosts
...
```
In the above example, there is a `/mnt/goofys` directory mounted as `goofys` filesystem.
