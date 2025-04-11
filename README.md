# kubernetes

## deploy cluster using manifest

### create aks cluster

```sh
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1  --generate-ssh-keys
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

### install an ingress controller

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

### deploy service to aks

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
helm package weatherforecast-api
```

### push chart to registry

```sh
helm registry login [container-registry] --username [user-name] --password [password]
helm push weatherforecast-api-<version>.tgz oci://[container-registry]/helm
az acr repository list --name [container-registry]
```

### create aks cluster

```sh
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 1  --generate-ssh-keys
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```

### install an ingress controller

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
```

### deploy service to aks (using helm from local)

```sh
kubectl get nodes
helm install weatherforecast-api weatherforecast-api/
kubectl get services
```

### deploy service to aks (using helm from registry)

```sh
kubectl get nodes
helm install weatherforecast-api oci://[container-registry]/helm/weatherforecast-api --version 0.1.0
kubectl get services
```