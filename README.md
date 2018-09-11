# Redis_in_Kubernetes
Use this repo to install redis as clusremode in Kubernetes.

## Follow Below Steps

1. Create namespace "redis" 
```
kubectl create namespace redis
```

2. Create configmap,svc and Statefulset 
```
kubectl create -f redis_config_svc_statefulset.yaml
```

3. Now check all pods are up or not. Once all pods are up and in running mode then run below command to setup cluster.
```
kubectl exec -it redis-cluster-0  -n redis -- redis-trib create --replicas 1 \
$(kubectl get pods -n redis -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')
```




 
