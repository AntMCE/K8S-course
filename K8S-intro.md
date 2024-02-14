# How is Kubernetes doing ?

https://www.cncf.io/reports/kubernetes-project-journey-report/

# How is Kubernetes organized ?



|  [**Steering Cometee**](https://github.com/kubernetes/steering#steering-committee) |  
|-----------------------|             
| [**SIG**](https://github.com/kubernetes/community/blob/master/sig-list.md)               | 
| **Work Groups**       |

      
                    


[Kubernetes Release Calendar](https://calendar.google.com/calendar/u/0/embed?src=agst.us_b07popf7t4avmt4km7eq5tk5ao@group.calendar.google.com&pli=1)



# Kubernetes Archtiecture

**kublet**: The kubelet is the primary "node agent" that runs on each node (create, edit, delete objects)

**etcd**: etcd is a strongly consistent, distributed key-value store that provides a reliable way to store data that needs to be accessed by a distributed system or cluster of machines. This is where the desired cluster configuration state is stored. That is the most sensitive / critical element of the Cluster.

**scheduler**: (Fliter & Score processes) The Kubernetes scheduler is a control plane process which assigns Pods to Nodes

**kube-api-server**: The Kubernetes API server validates and configures data for the api objects which include pods, services, replicationcontrollers, and others. The API Server services REST operations and provides the frontend to the cluster's shared state through which all other components interact

**controller Manager**: In Kubernetes, a controller is a control loop that watches the shared state of the cluster through the apiserver and makes changes attempting to move the current state towards the desired state.



![Alt text](<images/Cluster Architecture _ Kubernetes.png>)


## Inrteracting with a K8S Cluster 

![Alt text](<images/access control k8s.png>)


## Node Vs Pod Vs Container

![Alt text](<images/Viewing Pods and Nodes _ Kubernetes.png>)


**Node**: Host server

**Pod**: Entity that logically contains one or more containers that should be managed as a single entity.

*With the default maximum of **110 Pods per node** for Standard clusters, Kubernetes assigns a /24 CIDR block (256 addresses) to each of the nodes.*

**Container**: Instance of an image

**Namespace**: Namespaces are a way to organize clusters into virtual sub-clusters





## Services
Services: In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster

*3 types of services:*

**nodePort**: The NodePort service serves as the external entry point for incoming requests for your app

**clusterIP**: ClusterIP is the default service type in Kubernetes, and it provides **internal** connectivity between different components of our application

**loadBalancer**: The load balancer tracks the availability of pods with the Kubernetes Endpoints API. When it receives a request for a specific Kubernetes service, the Kubernetes load balancer sorts in order or round robins the request among relevant Kubernetes pods for the service

**Ingress**: Provision a load balancer and works as a reverse proxy (Layer 7)

**YAML Ports terminology:**

nodePort: external port on every cluster node

Port: Internal cluster port (service port)

targerPort: Port app listens on in Pods/Containers



## [API versioning](https://kubernetes.io/docs/reference/using-api/#api-versioning)

**Alpha**: For use only in short-lived testing

**Beta**: The software is not recommended for production uses

**Stable**: Production ready - The version name is vX where X is an integer.

**Kube No Trouble (kubent)** is a simple tool that helps you check your clusters for deprecated APIs. By configuring and running kubent, you'll be able to detect these deprecated APIs based on your deployments and be alerted on whether you should upload your workload first before upgrading your Kubernetes cluster.
[**Kubent**](https://docs.testkube.io/test-types/executor-kubent/)

![Alt text](<images/pod api stable.png>)


## 'kubectl get pods' mechanisme

1. **kubectl Invocation**: When you run kubectl, you're invoking the Kubernetes command-line interface (CLI). The kubectl command is a client-side tool that communicates with the Kubernetes API server.

2. **Configuration**: kubectl looks for its configuration file, typically located at ~/.kube/config. This configuration file contains details about the cluster, user credentials, and other settings that kubectl needs to communicate with the correct Kubernetes cluster.

3. **API Server Communication**: kubectl communicates with the Kubernetes API server specified in the configuration file. It sends a GET request to the /api/v1/pods to retrieve the list of pods from the default namespace.

4. **Authentication & Authorization**: Before the API server returns any data, it authenticates and authorizes the request. This ensures that the user making the request has the necessary permissions to access the requested resources.

5. **API Server Processing**: Once authenticated and authorized, the Kubernetes API server processes the request. It retrieves the list of pods from the etcd datastore (where cluster state is stored).

6. **Response**: The API server sends back a response containing information about the pods. This information includes details like pod name, status, IP address, and more.

7. **Display**: kubectl formats the response and displays it in the terminal. By default, it shows the pod names, their statuses, and other basic information.


## Pod creation mechanisme


kubectl apply -f mypod.yml --> API --> ETCD --> Scheduler -> Worker Node Kublet

The kubelet doesn’t create the Pod by itself. Instead, it delegates the work to three other components:

The Container Runtime Interface (CRI) — the component that creates the containers for the Pod.
The Container Network Interface (CNI) — the component that connects the containers to the cluster network and assigns IP addresses.
The Container Storage Interface (CSI) — the component that mounts volumes in your containers.



## Pod lifecycle


1. **Pending**: When a pod is created, it enters the Pending state. In this state, the Kubernetes scheduler is responsible for assigning the pod to a suitable node in the cluster. The scheduler considers factors like resource availability, node affinity, and pod anti-affinity when making this assignment.

2. **Running**: Once a pod is assigned to a node, it transitions to the Running state. In this state, the pod's containers are created and started, and they begin running on the assigned node. However, the containers may still be initializing or starting up, so the pod may not be fully ready to serve traffic.

3. **Succeeded**: If a pod completes its main task successfully and terminates, it enters the Succeeded state. This typically happens for batch jobs or one-time tasks. Once in the Succeeded state, the pod remains in this state until it is explicitly deleted. The resources occupied by the pod can be reclaimed by the system.

4. **Failed**: If a pod encounters an error or its containers fail to start or run, it enters the Failed state. This indicates a problem with the pod's execution. The pod will not be automatically restarted, but it can be manually deleted or recreated to address the failure.

5. **Unknown**: If the pod's status cannot be determined due to communication issues between the Kubernetes control plane and the pod's node, it enters the Unknown state. This can occur if the node becomes unresponsive or loses connectivity.






## Immutable and mutable fields

Immutable fields are usually metadata fields such as the name and namespace of an object, or fields that define the fundamental behavior of an object, such as its **API version, kind**, and **resource type**. For example, the **apiVersion, kind, "metadata . name**", and "**metadata** . **namespace**" fields are typically immutable in Kubernetes objects.

Mutable fields, on the other hand, are those that can be modified after an object has been created, such as the spec section of a Kubernetes object. This section typically contains configuration information such as the **number of replicas** for a deployment, the **port numbers** for a service, or the **container images** and **command** for a pod.



## Taints, Tolerations & Node affinity


