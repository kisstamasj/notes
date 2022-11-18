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
Acts as a front-end for kubernets. The users, managemenet devices and command line interfaces all talk to the api server

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

- ```kubectl create -f pod-definition.yml``` creates a pod|deployment (```--record``` records all the change)
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

# POD structure
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

## Example

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
Create multiple instance of pods. It can only handle that pods what it created itself.
## Example

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
Create multiple instance of pods.
There is a ```selector``` dictionary. Can manage other pods not just what it created itself.
## Example

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
When creating a new deployment it triggers a rollout, a rollout creates a new deployment revision (Revision 1)
When updating a deployment it will get a new deployment revision (Revision 2). It helps us keep tracking the changes, and it enables us to rollback to the previous version of deployment if neccessery.

- ```kubectl rollout status deployment/myapp-deployment``` get the deployment rollout statuses
- ```kubectl rollout history deployment/myapp-deployment``` get the deployment history and revisions

## Deployment Strategy
- Recreate: shut down the full application and recreate. The events will be cleard. !DANGEROUS!
- Rolling update: Not destroy the full application, update one by one of the services (This is the default strategy)

## Deployment upgrade
1. Create a new ReplicaSet
2. Rolling update the pods inside the ReplicaSet (shut down in the old ReplicaSet and create in the new ReplicaSet one by one)

## Deployment upgrade rollback
```kubectl rollout undo deployment/myapp-deployment```

## Example
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


