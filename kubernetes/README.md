# Kubernetes

## Overview

Kubernetes is an open-source container orchestration platform used to automate deployment, scaling, networking, and management of containerized applications.

It helps DevOps engineers manage applications running across multiple servers.


# Why Kubernetes is Important in DevOps

Kubernetes provides:

- Automated deployment
- Self-healing applications
- Container scaling
- Load balancing
- Rolling updates
- Resource management


# Kubernetes Architecture


## Control Plane

Responsible for managing the cluster.

Components:

- API Server
- Scheduler
- Controller Manager
- etcd


## Worker Nodes

Run application workloads.

Components:

- kubelet
- kube-proxy
- Container Runtime


# Core Kubernetes Objects Learned


## Pod

Smallest deployable unit in Kubernetes.

Contains one or more containers.


## Deployment

Manages application replicas and updates.


## Service

Provides stable network access to pods.


## Namespace

Logical separation of cluster resources.


## ConfigMap

Stores application configuration.


## Secret

Stores sensitive information.


# Kubernetes Networking

Learned:

- Pod networking
- Service networking
- Cluster communication
- Ingress


# Kubernetes Deployment Flow


Docker Image

↓

Container Registry

↓

Kubernetes Deployment

↓

Pods

↓

Service

↓

Users


# Operations Practiced

- Creating deployments
- Scaling applications
- Checking pod status
- Viewing logs
- Troubleshooting failed pods


# Troubleshooting Areas

- CrashLoopBackOff
- ImagePullBackOff
- Service connectivity issues
- Resource problems


# Related Technologies

- Docker
- Helm
- ArgoCD
- AWS EKS
- Monitoring tools