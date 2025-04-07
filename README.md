# kubernetes

## deploy cluster using manifest

### create aks cluster

```sh
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1  --generate-ssh-keys
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

### deploy cluster to aks

```sh
kubectl get nodes
kubectl apply -f manifest.yaml
kubectl get services
```

## deploy cluster using helm

### create chart

```sh
helm create weatherforecast-api
```

### package chart

```sh
helm package .
```

### push chart to registry

```sh
helm registry login [container-registry] --username [user-name] --password [password]
helm push weatherforecast-api-0.1.0.tgz oci://[container-registry]/helm
az acr repository list --name [container-registry]
```

### create aks cluster

```sh
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1  --generate-ssh-keys
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

### deploy cluster to aks (using helm from local)

```sh
kubectl get nodes
helm install weatherforecast-api weatherforecast-api/
kubectl get services
```

### deploy cluster to aks (using helm from registry)

```sh
kubectl get nodes
helm install weatherforecast-api oci://[container-registry]/helm/weatherforecast-api --version 0.1.0
kubectl get services
```