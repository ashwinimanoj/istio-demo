# Service Mesh Example with Istio 

## Setup 

### install istio 

we are using demo profile just to showcase istio's functionality

```
istioctl install -f istio-demo-config.yaml -y
```

### set istio injection in namespace

```
kubectl label namespace default istio-injection=enabled
```

### deploy ratings and booking service

```
kubectl apply -f bookinfo.yaml
```

```
kubectl get pods <pod-name> -o json | jq '.spec.containers[1].name'
```

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS productpage:9080/productpage | grep -o "<title>.*</title>"
```


### Setup gateway

```
kubectl apply -f gateway.yaml
```

```

### verify api call

```
curl -s "http://${GATEWAY_URL}/productpage" | grep -o "<title>.*</title>"
```