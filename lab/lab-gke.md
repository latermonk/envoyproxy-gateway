
# lab on GKE

https://www.cloudskillsboost.google/   

##  Choose the lab **Orchestrating the Cloud with Kubernetes**  

*Version list*
https://kubernetes.io/releases/          

```
gcloud container clusters create io --gateway-api=standard --location=us-central1-c   --cluster-version=1.27.3
```


https://gateway.envoyproxy.io/v0.5.0/user/quickstart/       



## Install
```
helm install eg oci://docker.io/envoyproxy/gateway-helm --version v0.5.0 -n envoy-gateway-system --create-namespace

```

```
kubectl wait --timeout=5m -n envoy-gateway-system deployment/envoy-gateway --for=condition=Available

```

```
kubectl apply -f https://github.com/envoyproxy/gateway/releases/download/v0.5.0/quickstart.yaml -n default

```

## Test
```
export GATEWAY_HOST=$(kubectl get svc/${ENVOY_SERVICE} -n envoy-gateway-system -o jsonpath='{.status.loadBalancer.ingress[0].ip}')

```

```
curl --verbose --header "Host: www.example.com" http://$GATEWAY_HOST/get

```

