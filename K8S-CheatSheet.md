## kubectl-really-get-all is a kubectl plugin that allows you to list every resource in your cluster (yes, really).
kubectl get all returns ONLY a list of pods, services, daemon sets, deployments, replica sets, jobs, cronjobs, and stateful sets

More: https://lnkd.in/g-TzypzS

## Get all the API resources available in the cluster
```
kubectl api-resources
```

## Interact with the container directly from the Worker / Master Nodes
```
crictl pull IMAGE-NAME
```
```
crictl images
```
```
crictl ps -a
```
```
crictl exec -it
```
```
crictl inspect
```
```
crictl logs
```
```
crictl pods
```

## Command "top" for K8S
```
kubectl top node    
```
```
kubectl top pod   
```
