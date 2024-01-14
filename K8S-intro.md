
# Kubernetes Archtiecture

**kublet**: The kubelet is the primary "node agent" that runs on each node (create, edit, delete objects)

**etcd**: etcd is a strongly consistent, distributed key-value store that provides a reliable way to store data that needs to be accessed by a distributed system or cluster of machines

**scheduler**: The Kubernetes scheduler is a control plane process which assigns Pods to Nodes

**kube-api-server**: The Kubernetes API server validates and configures data for the api objects which include pods, services, replicationcontrollers, and others. The API Server services REST operations and provides the frontend to the cluster's shared state through which all other components interact

**controller Manager**: In Kubernetes, a controller is a control loop that watches the shared state of the cluster through the apiserver and makes changes attempting to move the current state towards the desired state.



![Alt text](<images/Cluster Architecture _ Kubernetes.png>)


# Inrteracting with a K8S Cluster 

![Alt text](<images/access control k8s.png>)


# Node Vs Pod Vs Container

![Alt text](<images/Viewing Pods and Nodes _ Kubernetes.png>)


**Node**: Host server

**Pod**: Entity that logically contains one or more containers that should be managed as a single entity.

**Container**: instance of an image

**Namespace**: Namespaces are a way to organize clusters into virtual sub-clusters

**Services**: In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster

    3 types of services:

    Node Port:

    cluster IP:

    Load balancer:

**YAML terminology:**

nodePort: external port on every cluster node

Port: Internal cluster port (service port)

targerPort: Port app listens on in Pods/Containers



## Do you know what happens when you type 'kubectl get pods' and hit enter?


1. **kubectl Invocation**: When you run kubectl, you're invoking the Kubernetes command-line interface (CLI). The kubectl command is a client-side tool that communicates with the Kubernetes API server.

2. **Configuration**: kubectl looks for its configuration file, typically located at ~/.kube/config. This configuration file contains details about the cluster, user credentials, and other settings that kubectl needs to communicate with the correct Kubernetes cluster.

3. **API Server Communication**: kubectl communicates with the Kubernetes API server specified in the configuration file. It sends a GET request to the /api/v1/pods to retrieve the list of pods from the default namespace.

4. **Authentication & Authorization**: Before the API server returns any data, it authenticates and authorizes the request. This ensures that the user making the request has the necessary permissions to access the requested resources.

5. **API Server Processing**: Once authenticated and authorized, the Kubernetes API server processes the request. It retrieves the list of pods from the etcd datastore (where cluster state is stored).

6. **Response**: The API server sends back a response containing information about the pods. This information includes details like pod name, status, IP address, and more.

7. **Display**: kubectl formats the response and displays it in the terminal. By default, it shows the pod names, their statuses, and other basic information.
