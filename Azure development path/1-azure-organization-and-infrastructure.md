# Azure development path
# Azure Organization and Infrastructure

## Azure Global infrastructure
### Regions:
Each Azure region features datacenters deployed within a latency-defined perimeter. They're connected through a dedicated regional low-latency network. This design ensures that Azure services within any region offer the best possible performance and security.

### Availability zones
Failures can range from software and hardware failures to events such as earthquakes, floods, and fires. Tolerance to failures is achieved because of redundancy and logical isolation of Azure services. To ensure resiliency, a minimum of three separate availability zones are present in all availability zone-enabled regions.

Azure availability zones are connected by a high-performance network with a round-trip latency of less than 2ms. They help your data stay synchronized and accessible when things go wrong. Each zone is composed of one or more datacenters equipped with independent power, cooling, and networking infrastructure. Availability zones are designed so that if one zone is affected, regional services, capacity, and high availability are supported by the remaining two zones.
![image](https://user-images.githubusercontent.com/48266482/217852342-ca940eda-5f27-4489-85cc-2deacb890fe7.png)

Datacenter locations are selected by using rigorous vulnerability risk assessment criteria. This process identifies all significant datacenter-specific risks and considers shared risks between availability zones.

With availability zones, you can design and operate applications and databases that automatically transition between zones without interruption. Azure availability zones are highly available, fault tolerant, and more scalable than traditional single or multiple datacenter infrastructures.

Each data center is assigned to a physical zone. Physical zones are mapped to logical zones in your Azure subscription. Azure subscriptions are automatically assigned this mapping at the time a subscription is created. You can use the dedicated ARM API called: checkZonePeers to compare zone mapping for resilient solutions that span across multiple subscriptions.

You can design resilient solutions by using Azure services that use availability zones. Co-locate your compute, storage, networking, and data resources across an availability zone, and replicate this arrangement in other availability zones.

Azure availability zones-enabled services are designed to provide the right level of resiliency and flexibility. They can be configured in two ways. They can be either zone redundant, with automatic replication across zones, or zonal, with instances pinned to a specific zone. You can also combine these approaches.

Some organizations require high availability of availability zones and protection from large-scale phenomena and regional disasters. Azure regions are designed to offer protection against localized disasters with availability zones and protection from regional or large geography disasters with disaster recovery, by making use of another region. To learn more about business continuity, disaster recovery, and cross-region replication, see Cross-region replication in Azure.

![image](https://user-images.githubusercontent.com/48266482/217852737-f0a10b65-dc0c-481d-aa17-8c4628528c2a.png)


## Azure Services
### Platform services
- Media & CDN (Media services, Media analytics, Content Delivery Network)
- Application patform (Web apps, Mobile apps, API apps, Cloud services, Service Fabric, Notification hubs, Functions)
- Data (SQL databases, Azure Synapse Analytics, Cosmos DB, SQL Server Strech Dtabase, Azure Cache for Redis, Table Storage, Azure Search)
- Integration (API management, Service Bus, Azure Logic Apps)
- Compure Services (Container services, VM Scale Sets, Azure Batch, Dev/Test Lab)
- Developer services (Visual Studio, Azure DevOps, Application Insights, Mobile Engadgement, Xamarin, Visual Studio App Center)
- Analytics IoT

### Infrastucture service
- Compute (Virtual machines, Containers and Azure kubernetes)
- Storage (Blob, Queues, Files, Disks)
- Networking (Virtual network, Load Balancer, DNS, Express Route, Traffic Manager, VPN Gateway, App Gateway)

![image](https://user-images.githubusercontent.com/48266482/217858022-7b92f201-2208-42a5-9840-95df3a68d8e1.png)

### Iaas, PaaS and SaaS

![image](https://user-images.githubusercontent.com/48266482/217860079-e5b3f20d-4a9b-4a04-9126-93cd69d76a69.png)

#### IaaS
- Virtual servers
- you are responsible for maintaining OS

#### PaaS
- Cloud vendor maintains infrasturcure for you
- You focus on application code and data

#### SaaS
- Vendor provides full software stack

## Azure Resource Manager (ARM)
![image](https://user-images.githubusercontent.com/48266482/217863706-b122f164-177f-470e-b041-1928ecd7a38a.png)

## Azre Resource Hierarchy
![image](https://user-images.githubusercontent.com/48266482/218100072-071d11e1-297e-4e8b-9128-7be34d812bba.png)


### Fundamentals
- Parent-child relationship
- Access/policies granted to pranet inherited by child levels
- Centralized management
- Parent can have multiple children - child can only have one parent
- Similar to OS file structure

![image](https://user-images.githubusercontent.com/48266482/218101957-63ca5bf0-69d4-482e-8e8f-010d7251ce5d.png)

![image](https://user-images.githubusercontent.com/48266482/218102916-f3d6d54b-4e89-49b1-aa93-62a3501e5166.png)

## Identity and access management (IAM)

### Who can do what on which resources?
![image](https://user-images.githubusercontent.com/48266482/218103674-2cef454c-59df-4c0f-abbe-cf30a9440957.png)

### Azure Active Directory (Azure AD)
![image](https://user-images.githubusercontent.com/48266482/218105032-bd8570e7-b171-48a5-b5c0-77a5dea2e134.png)

### Azure Role-Based Access Control (Azure RBAC)
![image](https://user-images.githubusercontent.com/48266482/218105583-7b4937ad-6120-4464-85dd-a97510b0f71a.png)

### Scope
![image](https://user-images.githubusercontent.com/48266482/218105858-aaa3c44b-224e-473f-a065-0f7da51dab2a.png)

## Monitoring Azure Environment

- Logs (text-based)
  - Ativity logs: "Who created the resoure and when?"
  - OS Logs: "Why is windows giving an error?"
- Metrics (Telemetry-based performance data)
  - CPU utilization
  - Website latency

![image](https://user-images.githubusercontent.com/48266482/218106842-9a6d4025-238c-4fd7-843c-8082a6adba30.png)

## Core Services
### Virtual Machines (compute)
- IaaS
![image](https://user-images.githubusercontent.com/48266482/218398271-024ce87d-8d7c-4f96-a979-089a4b4ebb4f.png)
- Flexibility (you can do everything you want)
- Availability set
  - VM replication (copy)
  - Replicate VM for better faukt tolearance
  - If a VM goes down, a coped VM can take over
- Scale sets
  - Multiple copies of VMs
  - Scaling copies of application
  - Enables scaling, and elasticity 
### Networking
- Virtual network
- Load Balancer
- DNS
- Express Route
- Traffic Manager
- VPN Gateway
- App Gateway
#### Virtual network (VNet)
- Provides **private** and **public** network communication among Azure resources
- Uses familiar network concepts in virtual format: subnets, firewalls, routes, etc
  - Virtual format - **Software Defined Networking (SDN)**
  -  Enables public access or extends private networking to other networks

![image](https://user-images.githubusercontent.com/48266482/218400123-39d579a6-155d-4518-8df4-8861e45d5b8c.png)

- **Subnets**: Segment multiple resources for precise organisation
- **Peering/VPN/Express Route**: Connect to other Azure VNets across regions, on-premises networks, or other cloud networks
- **Network Security Groups/Firewall**: Control access to VNet resources by network protocol, port, or source locations

### Storage (Storage Accounts)
- Massivly scalable (petabytes and up)
- Managed infrasturcture (just store your stuff and go)
- Flexible access options
- Multiple data storage scenarios:
  - Blob (Binary Large Object)
    - Object storage
    - Unstructured data
    - All file types (image, video, scripts, etc..)
  - Files
    - Network file share in the cloud
  - Disks
    - Virtual hard drives for VMs ()
  - Queues
    - Asynchronous messaging between apps and services
  - Tables (...kind of)
    - NoSQL datrabase storage
    - Gradually transitioning to Cosmos DB

![image](https://user-images.githubusercontent.com/48266482/218402331-d1c0b7e8-c487-472b-bceb-b14538bbf0f9.png)

### Databases and Analytics
#### Databases
- Structured data
- PaaS

![image](https://user-images.githubusercontent.com/48266482/218404914-41575cc6-8447-433b-8812-d06753a8bbd9.png)

#### Analytics
- Analyzing data (in databases) for insights ("What are our most popular features?")
- Massive amounts of queried data ("How happy are our customers?")
- Ex.:
  - Azure Synapse (Query and visualization)
  - Azure Data Lake (Customer metrics)

### App Service and Serverless Compute
Azure handles all the resources that our app needs.
If we use VMs we have to deal with setting up the environment and all the necessary resources.

**Azure App service platform:**
- Web Apps
- Mobile Apps
- API Apps
- Cloud Services
- Service Fabric
- Notification Hubs
- Functions

**Trade flexibility for convinience**
- App Service supports multiple languages and containers, but VMs are more flexible

**Developer/coding focused tool**
- Non-developers will not get much use

## Azure Managed Services (Examples)
### Azure SQL 
#### Azure Manages:
- OS updates/patching
- Backups
#### You manage:
- Compute and storage configuration
- Loading and working with your data

Different managed services handle different management responsibilities
