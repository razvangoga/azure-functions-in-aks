# cluster setup

``` bash
kubectl create namespace az-func
kubectl create namespace keda

func kubernetes install --namespace keda # install KEDA in cluster - needs k8s connection info in the /.kube/config file
```

# deploy
``` bash
func init --docker-only # generate docker images for function
docker build -t func1 . # build function image
func kubernetes deploy --namespace az-func --name func1 --image-name func1
```

# generate k8s manifests
``` bash
func kubernetes install  --namespace keda --dry-run --namespace az-func  # dump KEDA yaml manifests
func kubernetes deploy --namespace az-func --dry-run --name func1 --image-name func1 # dump function yaml manifests
```