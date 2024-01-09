## Namespace that's stuck in the "terminating status":

1. Get all k8s resources that are stuck in the "terminating" stage in the Namespace and delete them.

Next, run the following commands:

```
kubectl get namespace NAMESPACE_NAME -o json > file.json
```
```
kubectl replace --raw "/api/v1/namespaces/NAMESPACE_NAME/finalize" -f ./file.json
```
After that, you should see that the Namespace can now be successfully deleted without sitting in the "Terminating" stage


## Get pod Events:
```
kubectl describe pod <pod-name> -n <namespace> | grep -A5 "Events:
```
