# Kubernetes Basics

Short repo summarizing basic kubernetes concepts and a short implementation of a cluster.

Tutorial showing basics:
[minikube hello-world tutorial](https://kubernetes.io/docs/tutorials/hello-minikube/)

**More extensive basic tutorial**
[kubernetes basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)

# Concepts

## What is Kubernetes
See [What is Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/ ).

![Difference between traditional, virtualized and container deployments.](/imgs/traditional_vs_virtualized_vs_container.png)

Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

Some of K8s features include:
- includes its own **load balancer** to balance load among pod containers.
- includes an **automatic bin-packing**: You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
- lets users integrate their **logging**, **monitoring**, and alerting solutions.

# Kubernetes Components

See [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/ ).

![Cluster](/imgs/cluster.png)

- A kubernetes **cluster** consists of **nodes** (physical machines or VMs).
- **Nodes** host one or several pods
- A pod is a group of one or more **containers**, and some **shared resources** for those containers.
- **Pods are the atomic unit** on the Kubernetes platform.

Cluster nodes             |  Node elements
:-------------------------:|:-------------------------:
![](/imgs/node_cluster.png)  |  ![](/imgs/node_overview.png)

- The **Control plane **manages the worker nodes, includes the **kube-scheduler**
- kube-scheduler **assigns new pods to nodes**.



## Pod

- By default, the Pod is only accessible by its internal IP address within the Kubernetes cluster.
- To make a **Container accessible from outside** the Kubernetes virtual network, you have to expose the Pod as a Kubernetes **Service**.
- **each Pod** in a Kubernetes cluster **has a unique IP** address, even Pods on the same Node
- A **Service** can be used to represent pods to the outside world and has a **fixed IP address**
