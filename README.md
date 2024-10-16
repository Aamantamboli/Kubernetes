# <div align="center"> Kubernetes </div>
<p align="center">
 <img src="https://github.com/user-attachments/assets/4927ba71-edc3-4342-a44e-ecab06bad28d"/>
</p>

## What is Kubernetes?
Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.Kubernetes is an open-source platform that automates the management, deployment, and scaling of containerized applications. It's also known as "k8s" or "k-eights", which comes from counting the eight letters between the "K" and the "s" in Kubernetes. 

## Kubernetes Architecture

![image](https://github.com/user-attachments/assets/02a15e4b-9b5a-4931-840a-787017d797f5)

Kubernetes is a powerful orchestration platform for managing containerized applications. Its architecture consists of several components that work together to ensure efficient deployment, scaling, and operation of applications. Here’s an overview of its key components:<br>
### 1. Master Node
The master node is responsible for managing the Kubernetes cluster. It runs several key components:<br>
**API Server:** The entry point for all administrative tasks. It exposes the Kubernetes API, which allows users to interact with the cluster.<br>
**Controller Manager:** Manages controllers that handle routine tasks, such as maintaining the desired state of the cluster (e.g., ensuring the number of replicas for a deployment).<br>
**Scheduler:** Assigns newly created pods to nodes based on resource availability and constraints.<br>
**etcd:** A distributed key-value store that stores all cluster data, including configurations and the current state of the cluster.<br>

### 2. Worker Nodes
These nodes run the actual applications in containers. Each worker node contains:<br>
**Kubelet:** An agent that communicates with the master node and ensures that containers are running as specified in the Pod definitions.<br>
**Kube Proxy:** Manages network communication to and from pods. It maintains network rules and helps load balance traffic to the pods.<br>
**Container Runtime:** The software responsible for running containers. Common options include Docker, containerd, and CRI-O.<br>

## Key Features of Kubernetes
### 1. Container Orchestration
Kubernetes manages clusters of containers, ensuring that the desired state of applications is maintained. It can automatically start, stop, and scale containers based on the specified requirements.
### 2. Scaling
Kubernetes can dynamically scale applications up or down based on demand. This is useful for handling varying workloads and ensuring efficient resource usage.
### 3. Load Balancing 
It provides built-in load balancing to distribute traffic across containers, ensuring optimal performance and availability.
### 4. Self-Healing
Kubernetes can automatically restart failed containers, replace and reschedule them, and manage the overall health of applications.
### 5. Service Discovery and Networking
Kubernetes facilitates service discovery by providing DNS for services and managing network policies for communication between containers.
### 6. Storage Orchestration
It can automatically mount the storage system of your choice, whether from local storage, public cloud providers, or networked storage solutions.
### 7. Configuration Management
Kubernetes manages application configurations and secrets, making it easier to deploy applications in different environments without hardcoding settings.
### 8. Multi-Cloud and Hybrid Deployments
Kubernetes supports running applications across various cloud providers and on-premises infrastructure, making it suitable for multi-cloud and hybrid environments.

## Objects of Kubernetes
In Kubernetes, the term "objects" refers to persistent entities in the system that represent the desired state of your applications and infrastructure. These objects are used to manage the various components of a Kubernetes cluster. Here are some of the key Kubernetes objects:
### 1. Pod
The smallest deployable unit in Kubernetes.<br>
A pod can contain one or more containers that share the same network namespace and storage.<br>
Pods are used to run applications and are often ephemeral in nature.<br>
### 2. Service
An abstraction that defines a logical set of pods and a policy to access them.<br>
Services enable stable networking and load balancing for pods, regardless of their underlying IP addresses.<br>
Common types include ClusterIP (default), NodePort, LoadBalancer, and ExternalName.<br>
### 3. Deployment
A higher-level object that manages a set of identical pods.<br>
It provides declarative updates for pods, allowing you to easily manage changes and rollbacks.<br>
You can specify the desired number of replicas and the container images to use.<br>
### 4. ReplicaSet
Ensures that a specified number of pod replicas are running at all times.<br>
It is often used by Deployments to manage the pod lifecycle, but can also be used independently.<br>
### 5. StatefulSet
Similar to Deployments, but used for managing stateful applications.<br>
Ensures that pods have unique identities and stable storage (using Persistent Volumes).<br>
Useful for applications like databases that require stable network identities.<br>
### 6. DaemonSet
Ensures that a copy of a pod runs on all (or some) nodes in the cluster.<br>
Commonly used for running cluster-wide services like logging agents or monitoring tools.<br>
### 7. Namespace
A way to divide cluster resources between multiple users or teams.<br>
Namespaces provide a scope for names, allowing you to create isolated environments within the same cluster.<br>
### 8. ConfigMap
Used to store non-confidential configuration data in key-value pairs.<br>
Allows you to decouple configuration artifacts from container images.<br>
### 9. Secret
Similar to ConfigMaps, but used for storing sensitive information (e.g., passwords, tokens).<br>
Secrets are encoded and can be made available to pods in a secure manner.<br>
### 10. PersistentVolume (PV)
Represents a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes.<br>
PersistentVolumes exist beyond the lifecycle of individual pods.<br>
### 11. PersistentVolumeClaim (PVC)
A request for storage by a user.<br>
It abstracts the underlying storage system, allowing users to request specific storage sizes and access modes.<br>
### 12. Ingress
Manages external access to services, typically HTTP.<br>
Provides features like load balancing, SSL termination, and name-based virtual hosting.<br>
