---
title: "Kubernetes-Basics"
layout: page
date: 2025-04-04
categories: [k8s]
permalink: /blog/k8s-basics/
---



# Kubernetes Basics

Kubernetes, often abbreviated as K8s, is an open-source platform designed to automate deploying, scaling, and operating application containers. Below are the key concepts and components of Kubernetes:

## Key Concepts

### 1. **Cluster**
A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one master node and multiple worker nodes.

### 2. **Node**
A node is a physical or virtual machine that runs the applications and is managed by the master node.

### 3. **Pod**
A pod is the smallest deployable unit in Kubernetes. It can contain one or more containers that share the same network namespace and storage.

### 4. **Service**
A service is an abstraction that defines a logical set of pods and a policy to access them. It provides stable networking for pods.

### 5. **Namespace**
Namespaces are used to divide cluster resources between multiple users or teams.

## Core Components

### 1. **Master Node**
The master node manages the Kubernetes cluster. It contains the following components:
- **API Server**: Exposes the Kubernetes API.
- **Controller Manager**: Ensures the desired state of the cluster.
- **Scheduler**: Assigns workloads to nodes.
- **etcd**: A distributed key-value store for cluster data.

### 2. **Worker Node**
The worker node runs the application workloads. It contains:
- **Kubelet**: Ensures containers are running in a pod.
- **Kube-proxy**: Manages networking for pods.
- **Container Runtime**: Runs the containers (e.g., Docker, containerd).

## Basic Commands

```bash
# Check cluster information
kubectl cluster-info

# List all nodes
kubectl get nodes

# Deploy an application
kubectl apply -f <deployment-file>.yaml

# Get all pods
kubectl get pods

# Delete a resource
kubectl delete -f <resource-file>.yaml
```

## Conclusion
Kubernetes simplifies container orchestration, making it easier to manage and scale applications. Understanding its basics is the first step toward mastering containerized application deployment.
