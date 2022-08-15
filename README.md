# Kubernetes Basics

Short repo summarizing basic kubernetes concepts and a short implementation of a cluster.

# Concepts

## What is Kubernetes
See [What is Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/ ).

![Difference between traditional, virtualized and container deployments.](/imgs/traditional_vs_virtualized_vs_container.png)

Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation.

Some of K8s features include:
- includes its own **load balancer** to balance load among pod containers.
- includes an **automatic bin-packing**: You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
- lets users integrate their **logging**, **monitoring**, and alerting solutions.
