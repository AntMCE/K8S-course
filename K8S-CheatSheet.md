# Everydays Command

Replace image in a deployment

```
kubectl set image deployment/my-deployment mycontainer=myimage:1.9.1
```

Create a yaml deployment template
```
k create deploy DEPLOYMENT_NAME --image=containous/whoami --port=80 --replicas=3 --dry-run=client -o yaml > deploy.yml
```
create a yaml sercive template
```
k create service nodeport ns-service --tcp=80:80 --dry-run=client -o yaml > svc.yml
```

Show labels of all pods in the namespace sun
```
k -n sun get pod --show-labels
```
Get pods in the namespace sun with existing label type=runner
```
k -n sun get pod -l type=runner
```
add the label protected=true to pod already having existing label type=runner.

```
k -n sun label pod -l type=runner protected=true 
```
Execute a curl from an ephemeral pod
```
k run tmp --restart=Never --rm --image=nginx:alpine -i -- curl http://svc-pod.axians:80
```
Start a debug pod which get deleted on exit

```
kubectl run debug --rm -ti --restart=Never --image=fedora:latest /bin/bash
```

delete all pods having the app=my-app label in the default namespace

```
k delete pods -l app=my-app -n default
```
To get the list of history of a specific deployment in a specific namespace
```
kubectl -n setra rollout history deploy client-dep
```
To rollout the deployment to REVISION 1 then use this command
```
kubectl -n setra rollout undo deploy client-dep --to-revision=1
```
Update the image container of a deployment in a specific namespace
```
kubectl -n setra set image deployment/sophia nginx=nginx:1.14.2:l
```
Restart a deployment using rollout
```
kubectl -n setra rollout restart deployment/sophia-app
```
Replace an object using an updated file
```
k -n setra replace -f deploy-sophia.yml
```
# kubectl-really-get-all is a kubectl plugin that allows you to list every resource in your cluster (yes, really).
kubectl get all returns ONLY a list of pods, services, daemon sets, deployments, replica sets, jobs, cronjobs, and stateful sets

More: https://lnkd.in/g-TzypzS

# Get all the API resources available in the cluster.
```
kubectl api-resources
```

# Interact with the container directly from the Worker / Master Nodes
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

# Command "top" for K8S
```
kubectl top node    
```
```
kubectl top pod   
```
#  Create a certificate + key as user trainee

## create key --> create csr --> API K8S --> download CRT from API --> use CRT + KET

```
openssl genrsa -out trainee.key 2048
```
```
openssl req -new -key trainee.key -out trainee.csr # only set Common Name = trainee
```
 create CertificateSigningRequest named trainee-csr.yml with base64 trainee.csr
https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests

```
cat trainee.csr | base64 -w 0
```
## Pass the certificate to the CertificateSigningRequest object 

```
 k create -f csr-trainee.yml
```
## The certificate should now be in pending Condition
```
k get csr  
```
```
k certificate approve trainee
```
## Copy the section  " certificate "
```
k get csr trainee -o yaml 
```
## Decode the certificate and pass it to the file trainee.crt

```
echo COPY PAST CERTIFICATE | base64 -d > trainee.crt
```

## add new KUBECONFIG
``` 
k config set-credentials trainee --client-key=trainee.key --client-certificate=trainee.crt --embed-certs
```
```
k config set-context trainee --cluster=kubernetes --user=trainee
```
```
k config view
```
```
k config get-contexts
```
```
k config use-context trainee
```

## You now need to make sure your user has the right permission via RBAC


# RBAC see the [RBAC folder](https://github.com/AnthonyMacle/K8S-course/tree/main/RBAC) in this repo to get the yml files
```
 k apply -f RBAC-ClusroleRole.yml
```
```
k apply -f RBAC-ClusroleRoleBinding.yml
```
```
k auth can-i list secrets --as username
```
# Cronjob & Job

[Cronjob template exemple](https://github.com/AnthonyMacle/K8S-course/tree/main/Cronjob)

Trigger a Kubernetes Scheduled Job manually
```
kubectl create job --from=cronjob/<cronjob-name> <job-name> -n <namespace-name>
```
