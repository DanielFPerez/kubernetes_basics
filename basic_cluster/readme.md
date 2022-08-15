# Basic Cluster

This example is created using the tutorial from [TechWorld with Nana: Kubernetes Crash Course](https://youtu.be/s_o8dwzRlu4?t=2479).

This tutorial makes a web-app and a MongoDB Database, making use of ConfigMaps and Secret.
Finally, it makes the application accessible from the outside by offering it as a service.

<img src="https://github.com/DanielFPerez/kubernetes_basics/blob/main/basic_cluster/webapp_cluster_arch.png" width="700">

## File creation order
All of the files have been completed with comments explaining their structural parts.
They should be read in the order in which they were created:
1. mongo-config.yaml : ConfigMap of the database specifying the DB url
2. mongo-secret.yaml: Secret file specifying environment variables
3. mongo.yaml: Database  Deployment and Service
4. webapp.yaml: Web-app Deployment and Service

## Create cluster

For creating the cluster, the **ConfigMap**s and **Secret**s must exist before the **Deployment**s (since the Deployments use these).

Follow these steps:

1. `hello`
