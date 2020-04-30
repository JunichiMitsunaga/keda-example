# keda-example

## Install KEDA
Follow the official KEDA guide https://keda.sh/deploy/

## Create Azure Resource

```sh
az group create --location <location> --name keda-example
az storage account create --name kedaexample --resource-group keda-example
```

Get connecionstring
```sh
az storage account show-connection-string --name kedaexample
```

## Create cluster
The deployment consists of 1 components:
- nginx pod that will be scaled up and down

```sh
kubectl apply -f .deploy/
```

## Azure Blob Storage example
To scale the nginx deployment using 
deploy the `ScaledObjects`:
```sh
kubectl -f apply .keda-hpa/
```

this should result in creation of a new `ScaledObjects` and new HPA
```sh
# kubectl get hpa
$ kubectl get ScaledObject -n keda-scale
NAME                      DEPLOYMENT    TRIGGERS     AGE
azure-blob-scaledobject   scale-nginx   azure-blob   28s
```