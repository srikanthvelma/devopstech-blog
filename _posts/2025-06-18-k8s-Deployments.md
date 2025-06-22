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

![k8s_deploy](images\k8s_deploy-1.jpg)

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
      name: myapp-nginx
      labels:
        app: myapp
        type: frontend
    spec:
      containers:
      - name: myapp-nginx
        image: nginx
        ports:
        - containerPort: 80

```
## Rolling Update and Rollback
When ever you create a first deployment k8s will trigger a rollout, creating a deployment with revison (rev 1). Later if you update application - let us say by changing container image version , it creates another rollout with new deployment with revision (rev 2). K8s maintains the revision history , by which roll back if we get any error by new deployment change.

## Deployment strategies

There 2 deployment strategies in k8s 
1. **Recreate**:
In this , when we have multiple replicas, it will delete old replicaset and creates new replicaset in place.It straightforward. but with this startegy we will get downtime of our application.
![k8s_deploy](images\k8s_deploy-2.jpg)

### Example
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
      name: myapp-nginx
      labels:
        app: myapp
        type: frontend
    spec:
      containers:
      - name: myapp-nginx
        image: nginx
        ports:
        - containerPort: 80
```

2. **Rolling Update**
In Rolling Update strategy new version is gradually replacing the old version without impacting our application.K8s incrementally creating new pods while scaling down the old pods.
![k8s_deploy](images\k8s_deploy-3.jpg)

When a deployment is created with multiple replicas (for example, five), Kubernetes automatically generates a ReplicaSet that manages pod creation. During an upgrade, a new ReplicaSet is created with the updated configuration while the old ReplicaSet gradually scales down.

If no strategy is specified, Kubernetes defaults to the rolling update strategy. The diagram below summarizes both "Recreate" and "Rolling Update" strategies
![k8s_deploy](images\k8s_deploy-4.jpg)

## Updating deployment

We can update the deployment in different ways
1. Modify the **deployment yaml file** and apply the deployment
2. we can directly do some changes to the deployment by commands
``` kubectl set image deployment/myapp-deployment nginx-container=nginx:1.9.1 ```

## Common Commands used in deployment
- Create a deployment from comannd
    ```
    kubectl create deployment myapp --image=nginx
    ```
- Create a deployment:
    ```
    kubectl apply -f deployment.yaml
    ```
- View deployments:
    ```
    kubectl get deployments
    ```
- View all
    ```
    kubecctl get all
    ```
- Edit a deployment from command
    ```
    kubectl edit deployemnt/myapp
    ```
- Scale the pods in the deployment
    ```
    kbectl scale --replicas=3 deployment/myapp
    ```
- View status of rolling update
  ```
  kubectl rollout status deployment/myapp
  ```
- View history of Rolling update
  ```
  kubectl rollout history deployment/myapp
  ```
- with revision number
  ```
  kubectl rollout history deployment/myapp --revision=2
  ```

- Update deployment (rolling update):
    ```
    kubectl set image deployment/my-app my-app-container=new-image:tag
    ```
- Rollback deployment:
    ```
    kubectl rollout undo deployment/my-app
    ```
## Deployment Example yaml with most used options
```yaml

apiVersion: apps/v1                      # Deployment API version
kind: Deployment                         # Resource type
metadata:                                # Metadata for the deployment
  name: my-app-deploy                    # Deployment name
  labels:
    app: my-app                          # Labels for the deployment
  annotations:                           # Annotations for the deployment
    description: "This is deployment"    # Description annotation
  namespace: my-namespace                # Namespace for the deployment
spec:                                    # Deployment specification
  replicas: 3                            # Number of replicas for the deployment
  selector:                              # Selector for the deployment
    matchLabels:                         # Match labels for the selector
      app: my-app                        # Label to match
  strategy:                              # Deployment strategy
    type: RollingUpdate                  # Strategy type
    rollingUpdate:                       # Rolling update configuration
      maxUnavailable: 1                  # Maximum unavailable pods during update
      maxSurge: 1                        # Maximum surge pods during update
  template:                              # Pod template for the deployment
    metadata:                            # Metadata for the pod template
      labels:                            # Labels for the pod template
        app: my-app                      # Label to match in the pod template
    spec:                                # Pod specification
      restartPolicy: Always              # Restart policy for the pods
      imagePullSecrets:                  # Image pull secrets for the pod
        - name: my-image-pull-secret     # Image pull secret name
      containers:                        # List of containers in the pod template
        - name: my-container             # Container name
          image: nginx:latest            # Container image
          ports:                         # Ports exposed by the container
            - containerPort: 80          # Port number
              protocol: TCP              # Protocol used by the port
          args:                          # Arguments for the container
            - --arg1=value1              # Argument 1
            - --arg2=value2              # Argument 2
          command:                       # Command to run in the container
            - /bin/sh                    # Command to execute
            - -c                         # Command option
            - echo "Hello, World!"       # Command to run
          env:                           # Environment variables for the container
            - name: MY_ENV_VAR           # Environment variable name
              value: "my-value"          # Environment variable value
          envFrom:                       # Environment variables from a ConfigMap or Secret
            - configMapRef:              # Reference to a ConfigMap
                name: my-config-map      # ConfigMap name
            - secretRef:                 # Reference to a Secret
                name: my-secret          # Secret name
          resources:                     # Resource requests and limits
            requests:                    # Resource requests
              memory: "64Mi"             # Memory request
              cpu: "250m"                # CPU request
            limits:                      # Resource limits
              memory: "128Mi"            # Memory limit
              cpu: "500m"                # CPU limit
          volumeMounts:                  # Volume mounts for the container
            - name: my-volume            # Volume name
              mountPath: /data           # Mount path in the container
            - name: my-secret-volume     # Secret volume name
              mountPath: /etc/
      volumes:                           # Volumes for the pod template
        - name: my-volume                # Volume name
          emptyDir: {}                   # Empty directory volume
        - name: my-secret-volume         # Secret volume name
          secret:                        # Secret volume configuration
            secretName: my-secret        # Secret name 
```

