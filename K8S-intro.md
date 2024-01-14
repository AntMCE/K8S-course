


![Alt text](<images/Cluster Architecture _ Kubernetes.png>)


![Alt text](<images/access control k8s.png>)

![Alt text](<images/Viewing Pods and Nodes _ Kubernetes.png>)










## Do you know what happens when you type 'kubectl get pods' and hit enter?


1. kubectl Invocation: When you run kubectl, you're invoking the Kubernetes command-line interface (CLI). The kubectl command is a client-side tool that communicates with the Kubernetes API server.

2. Configuration: kubectl looks for its configuration file, typically located at ~/.kube/config. This configuration file contains details about the cluster, user credentials, and other settings that kubectl needs to communicate with the correct Kubernetes cluster.

3. API Server Communication: kubectl communicates with the Kubernetes API server specified in the configuration file. It sends a GET request to the /api/v1/pods to retrieve the list of pods from the default namespace.

4. Authentication & Authorization: Before the API server returns any data, it authenticates and authorizes the request. This ensures that the user making the request has the necessary permissions to access the requested resources.

5. API Server Processing: Once authenticated and authorized, the Kubernetes API server processes the request. It retrieves the list of pods from the etcd datastore (where cluster state is stored).

6. Response: The API server sends back a response containing information about the pods. This information includes details like pod name, status, IP address, and more.

7. Display: kubectl formats the response and displays it in the terminal. By default, it shows the pod names, their statuses, and other basic information.