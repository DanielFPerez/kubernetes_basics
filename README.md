# Kubernetes Basics

Short repo summarizing basic kubernetes concepts and a short implementation of a cluster.

Tutorial showing basics:
[minikube hello-world tutorial](https://kubernetes.io/docs/tutorials/hello-minikube/)

**More extensive basic tutorial**
[kubernetes basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

# Concepts

## What is Kubernetes
See [What is Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/ ).

<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/traditional_vs_virtualized_vs_container.png" width="800">

Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

Some of K8s features include:
- includes its own **load balancer** to balance load among pod containers.
- includes an **automatic bin-packing**: You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
- lets users integrate their **logging**, **monitoring**, and alerting solutions.

## Kubernetes Components

See [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/).

<!--- ![Cluster](/imgs/cluster.png | width=3) --->
<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/cluster.png" width="800">

- A kubernetes **cluster** consists of **nodes** (physical machines or VMs).
- **Nodes** host one or several pods
- A pod is a group of one or more **containers**, and some **shared resources** for those containers.
- **Pods are the atomic unit** on the Kubernetes platform.

Cluster nodes             |  Node elements
:-------------------------:|:-------------------------:
<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/node_cluster.png" width="300"> | <img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/node_overview.png" width="300">

- The **Control plane** manages the worker nodes, includes the **kube-scheduler**
- kube-scheduler **assigns new pods to nodes**.



## Pod

- By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster.
- To make a **Container** **accessible** from outside the Kubernetes virtual network, you have to expose the Pod as a Kubernetes **Service**.
- Each **Pod** in a Kubernetes cluster **has a unique IP** address, even Pods on the same Node
- A **Service** can be used to represent pods to the outside world and has a **fixed IP address**

[Viewing Pods and Nodes](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore/explore-intro/)

Anything that the application would normally send to *STDOUT becomes logs* for the container within the Pod.
We can retrieve these logs using the **kubectl logs**


- Start a bash of a container in the pod:
`kubectl exec -ti $POD_NAME -- bash`

- Show logs
`kubectl logs $POD_NAME`


## What is kubectl?

CLI (command-line interface) command to interact with a kubernetes cluster. *NOTE*: the cluster must be already running.

Common format of a kubectl command is: `kubectl <action> <resource>`:
- **actions**: create, get, describe, etc.
- **resource**: node, container

*In order for kubectl to __find and access__ a Kubernetes cluster*, it needs a **kubeconfig** file, which is created automatically when you create a cluster using kube-up.sh or successfully deploy a Minikube cluster.

By default, kubectl configuration is located at `~/.kube/config`.

## Deployments

[What is a Kubernetes Deployment?](https://www.vmware.com/topics/glossary/content/kubernetes-deployment.html)
A Kubernetes **Deployment** is used to tell Kubernetes how to create or modify instances of the pods that hold a containerized application.

[Using kubectl to create a Deployment](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-app/deploy-intro/ )
The **kubectl** command can create a **proxy** that will forward communications into the cluster-wide, private network.
The proxy can be terminated by pressing Ctrl-C and won't show any output while its running.

In order for the new **Deployment** to be *accessible __without__ using the Proxy*, a **Service** is required

### Application Scaling

[Application Scaling tut](https://kubernetes.io/docs/tutorials/kubernetes-basics/scale/scale-intro/)
When traffic increases, we will need to scale the application to keep up with user demand.
Scaling is accomplished by changing the number of replicas in a Deployment

- Show deployment: `kubectl get deployments`
- Show **ReplicaSets**: `kubectl get rs`

Change number of replicas:
`kubectl scale deployments/$DEPL_NAME --replicas=4`
Would have this impact:
1 replica             |  4 replicas
:-------------------------:|:-------------------------:
<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/scaling_1.png" width="300"> | <img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/scaling_4.png" width="300">



## StateFulSets
A `StateFulSet` is a deployment for stateful applications.

## Service
[Using a Service to Expose your App](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/ )

Although each Pod has a unique IP address, those IPs are not exposed outside the cluster without a **Service**.

<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/services.png" width="650">

Services *allow your applications to receive traffic.*

Services can be exposed in different ways by specifying a type in the **ServiceSpec**.
- **ClusterIP** (default) - Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.
- **NodePort** - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using <NodeIP>:<NodePort>. Superset of ClusterIP.
- **LoadBalancer** - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. Superset of NodePort.
- **ExternalName** - Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up. This type requires v1.7 or higher of kube-dns, or CoreDNS version 0.0.8 or higher.

`kubectl expose $DEPLOYM_NAME --type=$TYPE --port $PORT`

**Service** routes traffic across a set of Pods.

Services are the abstraction that *allows pods to __die__ and __replicate__* in Kubernetes without impacting your application.

## ConfigMap and Secret

**ConfigMap** is a key-value store used for storing information accessible to your pods.
It could contain, e.g. a URL to expose your database that does not depend on the IP address of the Pod (which changes every time the Deployment shuts or instantiates a Pod).

**Secret** is like a ConfigMap for confidential information (e.g., user-password information).

<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/imgs/configmap_secret.png" width="600">
Image taken from [TechWorld with Nana: Kubernetes Crash Course](https://www.youtube.com/watch?v=s_o8dwzRlu4)
