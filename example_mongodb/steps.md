# deploy mongodb operator
```
helm install mongodb-operator ./path-to/mongodb-operator
```

# deploy mongodbservicetenant
```
kubectl apply -f mongodbservicetenant.yaml
```

# deploy tenant1
```
kubectl apply -f tenant1.yaml
```

# check composition
```
kubectl connections MongoDBServiceTenant tenant1 default -o png --ignore=ServiceAccount:default
```

# check policies
```
kubectl get pods example-mongodb-0 -n ns1 -o json | jq -r '.spec.containers[0].resources'
```

# check monitoring
### open terminal 1
```
kubectl port-forward  kubeplus -n default 8081:8090
```
### open terminal 2
```
curl -kv "http://127.0.0.1:8081/apis/kubeplus/metrics?kind=MongoDBServiceTenant&instance=tenant1&namespace=default"
```
