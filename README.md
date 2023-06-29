# Kubernetes core concepts
The purpose of Kubernetes is to contain your apps in "containers". This way you can deploy the app whenever, and to as many instances as required. It also allows for easy communication between services in your application. 
- Worker Nodes: They host the containers
- Master node: They define how and where the containers are stored, how they're moved. They manage the cluster.
- The cluster is composed of the worker nodes.

## Docker vs ContainerD
### Docker
Docker is a platform that provides a comprehensive set of tools and services for building, packaging and distributing containers. It includes Docker engine, which utilises ContainerD as its underlying runtime.

### ContainerD
It's an open source container runtime focused on core container functionality. It's designed to be lightweight, modular and easily embeddable into different container platforms and orchestration systems. 

## ETCD
It's a distributed key-value store that serves as the primary data store for storing and replicating critical cluster information. It provides the foundation for storing and accessing cluster configuration and state information in a distributed and highly available manner. 

- Data storage: It stores cluster-wide configuration data, including network settings, authentication details and API server configuration. 
- Consistency and reliability: It ensures data consistency and reliability.

## Kube-API Server
It acts as the primary interface for communication with the kubernetes cluster. It serves as the central control point for cluster administration, resource management and communication with other Kubernetes components. 

## Kube controller manager
The controllers are things that control certain things on the clusters, such as managing the containers, the number of worker nodes etc. They continuously monitor the state of certain parts of cluster, and look to fix parts. There are controllers to manage replicas, deployment, enpoints namespace and more. 

The controller manager has all of these controllers within it. When you install the controller manager, you get all of the individual controllers. 

## Kube scheduler
It decides which pod goes to which node, it can filter nodes based on metrics such as CPU etc. and then it can rank nodes based on how much resources the node has. (A pod is a group of one or more containers that are scheduled and run together on a cluster) It essentially decides which node the pods go to. 

## Kublet
It's the point of contact between other worker nodes and the master. Kubelets register nodes, create pods and monitors nodes and pods.

## Kube proxy
Every pod can communicate with every other pod using an internal pod network over the cluster. A service is created so the pods can be accessed, this also gets an IP address assigned to it. Whenever a pod tries to access a service using its IP or name, it forwards the traffic to the backend pod.

It acts as a network proxy, providing a virtual IP address for each service and distributing traffic to the appropriate backend pods. 

## Kube Pods
Pods are single instances of an application, one container instance per pod, they the smallest object you can create in Kubernetes. You can deploy multiple pods inside a node or launch a new node and pod.

Theres usually a 1 to 1 ration of pod and container. To scale within a node, you add more pods. You can have multiple containers in a pod, however they're usually different containers. 

## Pods with YAML
- When writing a YAML file, we have several essential parts:
    - apiVersion: v1 (We have multiple versions)
    ![](1.1.png)
    - kind: Pod (Again, we can have different kinds, like replicas)
    - metadata: (information about the object)
        - name: myapp-pod
        - labels:
            - app: myapp (key-value pair)
            - type: front-end
    - spec: (dictionary)
        - containers: 
            - name: nginx-controller
            - image: nginx (docker image name)
![](1.2.png)
- `kubectl get pods` shows the pods available

## Creating a pod definition file
- Make sure Docker is running, and Kubernetes is enabled.
- Open with `vim pod.yaml`
- Add the following:
![](1.3.png)
- Press `exit` and add `:wq`.
- Run the command `kubectl apply -f pod.yaml` to create the pod.
- `kubectl describe pod nginx` gives a detailed reading of nginx pod.
- When you run `kubectl get pods`, the ready section tells you how many containers are running. 
- In order to edit the vim file, we go into the file by calling its name. We can then use the `i` key, which allows us to edit.

## Replica sets
Replicas allow for high availability where you state a number of pods to run, and then the replication controller can bring up new pods to meet the replica set if any go down.
### Replication controller
A replication controller can control pods over multiple nodes.

- In order to do this, do the following yaml file:
![](1.4.png)
- Here, we're creating a replication controller. This allows us to create replicas of pods.
- The template that we are adding here is the metadata and spec for the individual pods for nginx.