# [Azure Architecture](https://learn.microsoft.com/hu-hu/training/paths/azure-fundamentals-describe-azure-architecture-services)

## Physical infrastructure
The physical infrastructure for Azure starts with datacenters. Conceptually, the datacenters are the same as large corporate datacenters. They’re facilities with resources arranged in racks, with dedicated power, cooling, and networking infrastructure.

As a global cloud provider, Azure has datacenters around the world. However, these individual datacenters aren’t directly accessible. Datacenters are grouped into Azure Regions or Azure Availability Zones that are designed to help you achieve resiliency and reliability for your business-critical workloads.

The [Global infrastructure](https://infrastructuremap.microsoft.com/) site gives you a chance to interactively explore the underlying Azure infrastructure.

## Regions 
An Azure region is a set of datacenters, deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network. With more global regions than any other cloud service provider, Azure gives customers the flexibility to deploy applications where they need. An Azure region has discrete pricing and service availability.

### "A set of datacenters"
Each region has more than one data center, which is a physical location.
Ex.: East US has an official location of Virginia, but there will be more than one datacenter there.

### "Latency defined perimeter"
Latency is the time it takes data to travel. Also means that datacenters are not "too far" from each other.

### Regional low-latency network
A fiber connection between data centers in the region.

## How to choose a region

### Location
Choose a region closest to your users to minimize latency.

### Features
Some features aren't in all regions. If you need a specific feature, some regions might be unavailable.

### Price
The price of services vary from region to region. 
Ex.: The price for a VM can be 20-30% difference  from region to region.

> You will often have to choose which is the most important: location, feature or price

## Paired Region
### Each Region is Paired
Paired within same geographic area except Brazil south.
Ex.: East US is paired with West US, France Central is paired with France South, Australia East is paired with Australia Southeast. The exception is Brazil South which is paired with South Central US.

### Outage Failover
If the primary region has an outage you can failover to the secondary region.
In the event of an outage affecting multiple regions, at least one region in each pair will be prioritized for recovery.

### Planned Updates
Only one region in a pair is updated at any one time.

### Replication 
Some services used paired regions for replication.

## Availability Zones
Availability zones are physically separate datacenters within an Azure region. Each availability zone is made up of one or more datacenters equipped with independent power, cooling, and networking. An availability zone is set up to be an isolation boundary. If one zone goes down, the other continues working. Availability zones are connected through high-speed, private fiber-optic networks.

![image](https://user-images.githubusercontent.com/48266482/223627489-ddb70c9c-01db-4fa9-a5a1-82cb111973f7.png)

> To ensure resiliency, a minimum of three separate availability zones are present in all availability zone-enabled regions. However, not all Azure Regions currently support availability zones.

### Physical Location
Each availability zone is a physical location within a region.

### Independent
Each zone has itsh own power, cooling and networking.

### Zones
Each region has a minimum of three zones.

![image](https://user-images.githubusercontent.com/48266482/219389259-6b108948-123b-4f73-a22d-e1a2e8a0efcd.png)

### Use availability zones in your apps
You want to ensure your services and data are redundant so you can protect your information in case of failure. When you host your infrastructure, setting up your own redundancy requires that you create duplicate hardware environments. Azure can help make your app highly available through availability zones.

You can use availability zones to run mission-critical applications and build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within an availability zone and replicating in other availability zones. Keep in mind that there could be a cost to duplicating your services and transferring data between availability zones.

Availability zones are primarily for VMs, managed disks, load balancers, and SQL databases. Azure services that support availability zones fall into three categories:

- Zonal services: You pin the resource to a specific zone (for example, VMs, managed disks, IP addresses).
- Zone-redundant services: The platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).
- Non-regional services: Services are always available from Azure geographies and are resilient to zone-wide outages as well as region-wide outages.
Even with the additional resiliency that availability zones provide, it’s possible that an event could be so large that it impacts multiple availability zones in a single region. To provide even further resilience, Azure has Region Pairs.

## Resource Groups
Every resource in Azure is in a Resource Group, there are no exceptions.

![image](https://user-images.githubusercontent.com/48266482/219393746-727782dd-047b-4653-8fdb-4ae8807d30a5.png)

> The resource group is not a resource.

### One Resource
Each resource can only exist on a single resource group.

### Add/Remove
You can add ore remove resources to any resource group at any time.

### Move resource: 
You can move a resourece from one resource group to another.

### Resource group delete
When a resource group is removed or deleted, all of the resources within it are deleted with it. You can remove resource groups at any time. To delete a resource group, you need access to the delete action. You also need delete for all resources in the resource group. If you have the required access, but the delete request fails, it may be because there's a lock on the resources or resource group. Even if you didn't manually lock a resource group, it may have been automatically locked by a related service. Or, the deletion can fail if the resources are connected to resources in other resource groups that aren't being deleted. For example, you can't delete a virtual network with subnets that are still in use by a virtual machine.

### Multiple Regions
Resources from multiple regions can be in one resource group. You could have a central database server in East US and your web application could be hosted in East US2, but they are in the same resource group, as they are related.

### Access Control
You can give users access to resource group and everything in it.

### Interact
Resources can interact with other resources in different resource groups.

### Location
A resource group has a location, or region, as it stores data about the resources in it.

## Azure Resource Manager (ARM)
Azure Resource Manager (ARM) is the underpinning of everything on Azure when it comes to createing, updateing, or deleting resources. It is deployment and management services for Azure. The key thing to knwo is that if you interact with any of the resources on Azure, it goes through the ARM.

![image](https://user-images.githubusercontent.com/48266482/219397084-898a0c18-305f-4cac-b47d-e485b0460987.png)

### ARM Benefits
####  Group Resource Handeling
You can deploy, manage and monitor resources as a group.

#### Consistency
Deploying resources from various tools will always result in the same consistent state.

#### Dependencies
Define dependencies between resources to make sure they don't get in a fight.

#### Access Control
Built-in features in the ARM make it easy to assign access rights users.

#### Tagging 
Tag resources to easily identify them for future scenarios. Tagging is a way to label individual resources.

#### Billing
Use tagging to stay on top of billing for groups of resource.



