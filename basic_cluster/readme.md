# Basic Cluster

This example is created using the tutorial from [TechWorld with Nana: Kubernetes Crash Course](https://youtu.be/s_o8dwzRlu4?t=2479).

This tutorial makes a web-app and a MongoDB Database, making use of ConfigMaps and Secret.
Finally, it makes the application accessible from the outside by offering it as a service.

# Install Container Runtime

Kubernetes requires a container runtime. For this, we install Docker, which also includes the [containerd runtime](https://containerd.io/).

Installation is done according to the Dcoker documentation for Ubuntu: [Installing Using the repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository).
Remember to execute the [post-installation](https://docs.docker.com/engine/install/linux-postinstall/) instructions, which creates a `docker` linux group to use docker as non-root.

# minikube

minikube is a light-weight kubernetes for running a cluster only in one local machine.

Installing minikube: https://minikube.sigs.k8s.io/docs/start/ 

# kubeadm

Full kubernetes cluster creation tool to create cluster across several machines.

Installing kubeadm: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
