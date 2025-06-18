---
title: "k8s-Deployments"
layout: post
date: 2025-06-18
categories: [k8s]
permalink: /blog/k8s/k8s-Deployments
tags: [kubernetes, k8s, cluster]
---

# Kubernetes Deployments

## Deployments
Lets us assume we have a web server in production , which needs to be run reliably without any distrubance. For this to happen we require multiple instances of this web server to distribute the load and for high availability. Moreover, when a new version is available for this, we need to update the version without web server down - this is caaled as **Rolling Update** and after update if new version gets any error we need to immediately reverse it - **Roll Back** and additionally if we want to manage and control any other various aspects of our environment, such as web server versions, deployment scaling , resource allocations.

While individual Pods run your application instances, ReplicaSets (or Replication Controllers) manage these Pods, ensuring the correct number are always running. A Deployment builds on these components by offering a higher-level abstraction. It not only handles rolling updates and rollbacks but also lets you pause and resume deployments as needed. It also handles the resource allocation like ,on which node our pod has to be loaded , any volume attachments.

![k8s_deploy](\assets\images\k8s_deploy-1.jpg)

- A **Deployment** in Kubernetes manages a set of identical pods.
- It is built on top of Pod and ReplicaSet.
- Ensures the desired number of pod replicas are running at all times.
- Supports rolling updates and rollbacks.
- Volume can be attached.

## Key Features
- **Declarative updates**: Define the desired state in YAML/JSON.
- **Self-healing**: Automatically replaces failed or terminated pods.
- **Scaling**: Easily scale pods up or down.
- **Rollback**: Revert to previous versions if needed.

## Basic Deployment YAML Example - Nginx
```yaml
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: myapp-nginx
  labels:
    app: myapp
    type: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      app: myapp
      type: frontend
    spec:
      containers:
      - name: myapp-nginx
        iamge: nginx
        ports:
        - containerPort: 80

```

## Common Commands
- Create a deployment:
    ```
    kubectl apply -f deployment.yaml
    ```
- View deployments:
    ```
    kubectl get deployments
    ```
- Update deployment (rolling update):
    ```
    kubectl set image deployment/my-app my-app-container=new-image:tag
    ```
- Rollback deployment:
    ```
    kubectl rollout undo deployment/my-app
    ```

## Best Practices
- Use labels and selectors carefully.
- Monitor rollout status.
- Use resource requests/limits.
- Version your container images.
