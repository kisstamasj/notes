## Documentation for learning and building a complex distributive system architecture
These document are a collection of well sorted links and code parts to learn services, technologies and programming languages like
- [Typescript](./NextJS.md)
- [NextJS](./NextJS.md)
- [NestJS](./NestJS%20-%20Microservices.md)
- APIs
- [Microservices](./microservices-useful-links.md)


# Table of Contents 
- ### [Kubernetes (K8s)](./k8s-basic.md)
  - **[Udemy course notes](./k8s-basic.md#Udemy-course-notes)**
  - **[K8s architecture](./k8s-basic.md#K8s-architecture)**
  - **[K8s components](./k8s-basic.md#K8s-components)**
    - [API server: ](./k8s-basic.md#API-server)
    - [etcd key store](./k8s-basic.md#etcd-key-store)
    - [kubelet:](./k8s-basic.md#kubelet)
    - [container runtime](./k8s-basic.md#container-runtime)
    - [controller](./k8s-basic.md#controller)
    - [scheduler](./k8s-basic.md#scheduler)
  - **[kubectl (kube control)](./k8s-basic.md#kubectl-(kube-control))**
    - [kubectl commands](./k8s-basic.md#kubectl-commands)
  - **[Installing](./k8s-basic.md#Installing)**
  - **[Useful Docker Desktop extensions](./k8s-basic.md#Useful-Docker-Desktop-extensions)**
  - **[VSCode extensions](./k8s-basic.md#VSCode-extensions)**
  - **[YAML structure](./k8s-basic.md#YAML-structure)**
  - **[POD Example](./k8s-basic.md#POD-Example)**
  - **[Replication controller](./k8s-basic.md#Replication-controller)**
    - [Replication controller Example](./k8s-basic.md#Replication-controller-Example)
  - **[ReplicaSet](./k8s-basic.md#ReplicaSet)**
    - [ReplicaSet Example](./k8s-basic.md#ReplicaSet-Example)
  - **[Deployments](./k8s-basic.md#Deployments)**
    - [Rollout and versioning](./k8s-basic.md#Rollout-and-versioning)
    - [Deployment Strategy](./k8s-basic.md#Deployment-Strategy)
    - [Deployment upgrade](./k8s-basic.md#Deployment-upgrade)
    - [Deployment upgrade rollback](./k8s-basic.md#Deployment-upgrade-rollback)
    - [Deployment Example](./k8s-basic.md#Deployment-Example)
  - **[Kubernetes networking](./k8s-basic.md#Kubernetes-Networking)**
  - **[Kubernetes services](./k8s-basic.md#kubernetes-services)**
    - [Services types](./k8s-basic.md#services-types)
      - [NodePort example](./k8s-basic.md#nodeport-example)
      - [ClusterIP example](./k8s-basic.md#clusterip-example)
      - [LoadBalancer example](./k8s-basic.md#loadbalancer-example)

- ### [NextJS](./NextJS.md)
  - **[TypeScript basics](./NextJS.md#TypeScript-basics)**
  - **[React basics](./NextJS.md#React-basics)**
  - **[NextJS](./NextJS.md#NextJS)**
  - **[UI FrameWorks](./NextJS.md#FrameWorks)**

- ### [NestJS - Microservices](./NestJS%20-%20Microservices.md)
  - **[Initialize project](./NestJS%20-%20Microservices.md#Initialize-project)**
    - [Project structure](./NestJS%20-%20Microservices.md#Project-structure)
    - [Common Library](./NestJS%20-%20Microservices.md#Common-Library)
    - [DevOps](./NestJS%20-%20Microservices.md#DevOps)
      - [NestJS docker image for a service:](./NestJS%20-%20Microservices.md#NestJS-docker-image-for-a-service)
      - [Service deployment yaml:](./NestJS%20-%20Microservices.md#Service-deployment-yaml)
      - [Event Broker with RabbitMQ - deployment yaml](./NestJS%20-%20Microservices.md#Event-Broker-with-RabbitMQ---deployment-yaml)
      - [Ingress service](./NestJS%20-%20Microservices.md#Ingress-service)
    - [Basic dependencies](./NestJS%20-%20Microservices.md#Basic-dependencies)
    - [Database dependencies (postgres)](./NestJS%20-%20Microservices.md#Database-dependencies-(postgres))
    - [Authentication dependencies](./NestJS%20-%20Microservices.md#Authentication-dependencies)
- ### [Useful links for microservices](./microservices-useful-links.md)
- ### [Azure development path](./Azure%20development%20path/azure-organization-and-infrastructure.md)
  * [Azure Organization and Infrastructure](#azure-organization-and-infrastructure)
    * [Azure main strengths and weaknesses](#azure-main-strengths-and-weaknesses)
      * [Strengths](#strengths)
      * [Weaknesses](#weaknesses)
    * [Real world use cases for azure](#real-world-use-cases-for-azure)
    * [Azure Global infrastructure](#azure-global-infrastructure)
      * [Regions:](#regions)
      * [Availability zones](#availability-zones)
    * [Azure basic pillars](#azure-basic-pillars)
    * [Azure Services](#azure-services)
      * [Platform services](#platform-services)
      * [Infrastucture service](#infrastucture-service)
      * [Iaas, PaaS and SaaS](#iaas-paas-and-saas)
         * [IaaS](#iaas)
         * [PaaS](#paas)
         * [SaaS](#saas)
    * [Azure Resource Manager (ARM)](#azure-resource-manager-arm)
    * [Azure Resource Hierarchy](#azure-resource-hierarchy)
        * [Fundamentals](#fundamentals)
    * [Identity and access management (IAM)](#identity-and-access-management-iam)
        * [Who can do what on which resources?](#who-can-do-what-on-which-resources)
        * [Azure Active Directory (Azure AD)](#azure-active-directory-azure-ad)
        * [Azure Role-Based Access Control (Azure RBAC)](#azure-role-based-access-control-azure-rbac)
        * [Scope](#scope)
    * [Monitoring Azure Environment](#monitoring-azure-environment)
        * [Azure Chaos studio](#azure-chaos-studio)
    * [Core Services](#core-services)
        * [Virtual Machines (compute)](#virtual-machines-compute)
        * [Networking](#networking)
        * [Virtual network (VNet)](#virtual-network-vnet)
        * [Storage (Storage Accounts)](#storage-storage-accounts)
        * [Databases and Analytics](#databases-and-analytics)
        * [Databases](#databases)
        * [Analytics](#analytics)
        * [App Service and Serverless Compute](#app-service-and-serverless-compute)
    * [Azure Managed Services (Examples)](#azure-managed-services-examples)
        * [Azure SQL](#azure-sql)
        * [Azure Manages:](#azure-manages)
        * [You manage:](#you-manage)
        * [Container/Kubernetes services](#containerkubernetes-services)
        * [Artificial Intelligence/Machine Learning](#artificial-intelligencemachine-learning)
        * [Big Data Solutions](#big-data-solutions)
        * [Internet of Things (IoT) Solutions](#internet-of-things-iot-solutions)
    * [Cloud Advantages](#cloud-advantages)
        * [How?](#how)
