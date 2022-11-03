# Udemy course notes

[Kubernetes+For+Beginners+-+Mumshad+Mannambeth.pdf](https://github.com/kisstamasj/documents/files/9926473/Kubernetes%2BFor%2BBeginners%2B-%2BMumshad%2BMannambeth.pdf)

# K8s architecture

- cluster (set of nodes together)
  - Node (virtual or physical machine)
    - pods (single instance of an application)

- master node (manage other nodes)
  - etcd
  - controller
  - scheduler
  - kube-apiserver
- worker node (container runtime)

# K8s components

### API server: 
Acts as a front end for kubernets. The users, managemenet devices, command line interfaces all talk to the api server

### etcd key store
Key-value store to store all data used to manage the cluster. Making sure that the containers are running on the nodes as expected.

### kubelet:
Its an agent that runs on each node in the cluster.

### container runtime
Underlying software that used to run containers.(Docker)

### controller
Brain behind orchestration. They are responsible for noticing and responding when nodes, containers or end points goes down.

### scheduler
Responsible distributed works accross multiple nodes.

# kubectl (kube control)
Is a tool to deploy and manage applications on a kubernets cluster.

- ```kubectl run nginx --image=nginx``` deploy an application on the cluster
- ```kubectl cluster-info``` get information about the cluster
- ```kubectl get nodes``` list of all nodes

# Installing
- enable Kubernetes on Docker Desktop
- install kubectl: https://kubernetes.io/docs/tasks/tools/
