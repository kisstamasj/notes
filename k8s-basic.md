<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
TOC

- [Udemy course notes](#udemy-course-notes)
- [K8s architecture](#k8s-architecture)
- [K8s components](#k8s-components)
    - [API server:](#api-server)
    - [etcd key store](#etcd-key-store)
    - [kubelet:](#kubelet)
    - [container runtime](#container-runtime)
    - [controller](#controller)
    - [scheduler](#scheduler)
- [kubectl (kube control)](#kubectl-kube-control)
  - [kubectl commands](#kubectl-commands)
- [Installing](#installing)
- [Useful Docker Desktop extensions](#useful-docker-desktop-extensions)
- [VSCode extensions](#vscode-extensions)
- [YAML Structure](#yaml-structure)
  - [POD Example](#pod-example)
- [Replication controller](#replication-controller)
  - [Replication controller Example](#replication-controller-example)
- [ReplicaSet](#replicaset)
  - [ReplicaSet Example](#replicaset-example)
- [Deployments](#deployments)
  - [Rollout and versioning](#rollout-and-versioning)
  - [Deployment Strategy](#deployment-strategy)
  - [Deployment upgrade](#deployment-upgrade)
  - [Deployment upgrade rollback](#deployment-upgrade-rollback)
  - [Deployment Example](#deployment-example)
- [Kubernetes Networking](#kubernetes-networking)
- [Kubernetes services](#kubernetes-services)
  - [Services types](#services-types)
    - [NodePort Example](#nodeport-example)
    - [ClusterIP Example](#clusterip-example)
    - [LoadBalancer Example](#loadbalancer-example)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# Udemy course notes

[Kubernetes+For+Beginners+-+Mumshad+Mannambeth.pdf](https://github.com/kisstamasj/documents/files/9926473/Kubernetes%2BFor%2BBeginners%2B-%2BMumshad%2BMannambeth.pdf)

# K8s architecture

- cluster (set of nodes together)
  - Node (virtual or physical machine)
    - pods (single instance of an application) https://kubernetes.io/docs/concepts/workloads/pods/

![image](https://user-images.githubusercontent.com/48266482/199826380-4ff71576-6bcb-4958-85b1-d47d64d31786.png)


- master node (manage other nodes)
  - etcd
  - controller
  - scheduler
  - kube-apiserver
- worker node (container runtime)

# K8s components

### API server: 
Acts as a front-end for kubernetes. The users, managemenet devices and command line interfaces all talk to the api server

### etcd key store
Key-value store to store all data used to manage the cluster. Making sure that the containers are running on the nodes as expected.

### kubelet:
It's an agent that runs on each node in the cluster.

### container runtime
Underlying software that is used to run containers.(Docker)

### controller
Brain behind orchestration. They are responsible for noticing and responding when nodes, containers or end points are going down.

### scheduler
Responsible for distributing works accross multiple nodes.

# kubectl (kube control)
Is a tool to deploy and manage applications on a kubernetes cluster.

## kubectl commands
- ```kubectl run nginx --image=nginx``` deploys an application on the cluster
- ```kubectl run nginx --image=nginx --dry-run=client -o yaml > nginx.yaml``` generates a yaml configuration file

- ```kubectl cluster-info``` gets information about the cluster
 
- ```kubectl get nodes``` lists all nodes
- ```kubectl get pods``` lists all pods (```-o wide``` param gives more informations)
- ```kubectl get replicaset``` lists all replicaset
- ```kubectl get deployment``` lists all deployments
- ```kubectl get all``` lists all created object (pods, services, deployments, replicaset)

- ```kubectl create -f pod-definition.yml``` creates a pod|deployment (```--record``` records all the change as events in the history (it is deprecated))
- ```kubectl apply -f pod-definition.yml``` creates/updates a pod|deployment (same as create)
- ```kubectl replace -f replicaset-definition.yml``` replaces the current instance of a yaml
- ```kubectl edit  <replicaset|pod|deployment> the-name-of-the-object``` edits the currently running object
- ```kubectl scale --replicas=6 -f replicaset-definition.yml``` scales up/down the replicaset (with 6 replica)
- ```kubectl scale replicaset myapp-replicaset --replicas=2```scales up/down the replicaset (with 2 replica)
- ```kubectl describe pod <pod-NAME>``` describes detaild information about a pod

- ```kubectl rollout status deployment.apps/<name-of-deployment>``` gets the deployment rollout statuses
- ```kubectl rollout history deployment.apps/<name-of-deployment>``` gets the deployment history and revisions
- ```kubectl rollout undo deployment.apps/<name-of-deployment>``` rolls back to the previous revision of a deployment

- ```kubectl delete pod nginx``` deletes the given pod
- ```kubectl delete replicaset myapp-replicaset``` deletes the given replicaset
- ```kubectl delete replicationController myapp-rc``` deletes the given replication controller


# Installing
- enable Kubernetes on Docker Desktop
- install kubectl: https://kubernetes.io/docs/tasks/tools/

# Useful Docker Desktop extensions
- Microcks (Mock API-s for microservises)
- Portainer (manage containers and kubernetes cluster)
- Snyk (check docker image vulnerabilities)

# VSCode extensions
- YAML: 
settigns:
```json
"yaml.schemas": {
    "kubernetes": "*.yaml"
  }
```
- Kubernetes

# YAML Structure
- apiVersion: kubernetes API version
  - POD: v1
  - Service: v1
  - ReplicaSet: apps/v1
  - Deployment: apps/v1
- kind: type of object what we create
  - POD
  - ReplicaSet
  - Deployment
  - Service
- metadata: data about the object
  - name: myapp-pod
  - labels: It can have any key and values. For example it can helps to organize pods in several groups 
    - app: myapp
    - etc...
- spec: informations about the objects, it can be different in different objects

## POD Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end
spec:
  containers:
    - name: nginx-container
      image: nginx

```

# Replication controller
Creates multiple instance of pods. It can only handle that pods what it created itself.
## Replication controller Example

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
       containers:
         - name: nginx-container
           image: nginx
  replicas: 3
```

# ReplicaSet
Creates multiple instance of pods.
There is a ```selector``` dictionary. Can manage other pods not just what it created itself.
## ReplicaSet Example

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-replicaset
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
       containers:
         - name: nginx-container
           image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```

# Deployments
![image](https://user-images.githubusercontent.com/48266482/202649900-583ce861-72fe-4015-a529-fc5418efc05a.png)
- Create deployment
- Deploy PODs
- Create Replica Set

## Rollout and versioning
When we are creating a new deployment it triggers a rollout, the rollout creates a new deployment revision (Revision 1)
When we are updating a deployment it will get a new deployment revision (Revision 2). It helps us keep tracking the changes, and it enables us to rollback to the previous version of the deployment if neccessery.

- ```kubectl rollout status deployment/myapp-deployment``` gets the deployment rollout statuses
- ```kubectl rollout history deployment/myapp-deployment``` gets the deployment history and revisions

## Deployment Strategy
- Recreate: shuts down the full application and recreates. The events will be cleard. !DANGEROUS!
- Rolling update: it doesn't destroy the full application but updates the services, one by one (This is the default strategy)

## Deployment upgrade
1. Creates a new ReplicaSet
2. Rolls an update to the pods inside the ReplicaSet (it shuts down the old ReplicaSet and creates a new one)

## Deployment upgrade rollback
```kubectl rollout undo deployment/myapp-deployment```

## Deployment Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-replicaset
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app: myapp
        type: front-end
    spec:
       containers:
         - name: nginx-container
           image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```

# Kubernetes Networking
- Nodes has own IP addresses
- PODs attatched to a private network (10.0.0.0)
- IP addresses is assigned to all PODs
- All containers/PODs can communicate to one another without NAT
- All nodes can cmommunicate with all containers and vice-versa without NAT

# Kubernetes services
It is also a kubernetes object like POD, Deployment or ReplicaSet. Kubernetes services enable communication between various components within and outside of the application. Services has own IP address called Cluster IP of the service. It works also with multiple nodes.

![image](https://user-images.githubusercontent.com/48266482/203935334-272dfb05-8e07-45a5-9830-4c38fc6db331.png)

This shows how its work a NodePort

## Services types
- NodePort: Makes an internal port accessibble on a port on the node.
  - Three ports: 
    - TargetPort: Where the service forwards the request to. For example a webserver listening on. (ex.: 80)
    - Port: The port on the service it self
    - NodePort: Use to access for example a webserver extrenally. Available range is 30000-32767.
 
 ![image](https://user-images.githubusercontent.com/48266482/203940337-f9f5a621-8d7e-4b22-84b1-f59de83bb16c.png)

- ClusterIP: Creates a virtual IP inside the cluster to enable communication between different services, such as a set of frontend servers to a set of backend servers.
- LoadBalancer: It provisions a load balancer for our application in supported cloud providers (GCP, AWS, Azure etc.). It gives simple access to a POD wich runs in more than one instance.

### NodePort Example
```yaml
apiVersion: v1
kind: Service
metadata: 
  name: myapp-service
spec:
  type: NodePort
  ports:
    - targetPort: 80 # Port exposed by the container
      port: 80 # Port on the service
      nodePort: 30008 # Port to access from outside
  # Matching NodePort service with POD with labels
  selector:
     app: app
     type: front-end
```

### ClusterIP Example
```yaml
apiVersion: v1
kind: Service
metadata: 
  name: back-end
spec:
  # ClusterIP is the default service type, so not necessary to define
  type: CulsterIP
  ports:
    - targetPort: 80 # Port exposed by the container
      port: 80 # Port on the service
  # Matching NodePort service with POD with labels
  selector:
     app: app
     type: back-end
```

### LoadBalancer Example
```yaml
apiVersion: v1
kind: Service
metadata: 
  name: myapp-service
spec:
  type: LoadBalancer
  ports:
    - targetPort: 80 # Port exposed by the container
      port: 80 # Port on the service
      nodePort: 30008 # Port to access from outside
  # Matching NodePort service with POD with labels
  selector:
     app: app
     type: back-end
```

