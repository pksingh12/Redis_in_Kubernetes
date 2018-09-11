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

4. Steps to validate cluster
```
* login to one of the pod and run below commands
  1. redis-cli -c info           => you should be able to see slaves are connected
  2. redis-cli -c cluster nodes  => you should be able to see all masters and slaves
```

5. More debugging
```
if you want to test its able to write keys or not use below commands to set and get keys
  1. redis-cli -c set "keyname" "valuename"    => to set keys
  2. redis-cli -c get "keyname"
```




 
