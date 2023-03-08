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
Most Azure regions are paired with another region within the same geography (such as US, Europe, or Asia) at least 300 miles away. This approach allows for the replication of resources across a geography that helps reduce the likelihood of interruptions because of events such as natural disasters, civil unrest, power outages, or physical network outages that affect an entire region. For example, if a region in a pair was affected by a natural disaster, services would automatically fail over to the other region in its region pair.

> **Important**
> 
> Not all Azure services automatically replicate data or automatically fall back from a failed region to cross-replicate to another enabled region. In these scenarios, recovery and replication must be configured by the customer.

### Each Region is Paired
Paired within same geographic area except Brazil south.
Ex.: East US is paired with West US, France Central is paired with France South, Australia East is paired with Australia Southeast. The exception is Brazil South which is paired with South Central US.

### Additional advantages of region pairs:
- If an extensive Azure outage occurs, one region out of every pair is prioritized to make sure at least one is restored as quickly as possible for applications hosted in that region pair.
- Planned Azure updates are rolled out to paired regions one region at a time to minimize downtime and risk of application outage.
- Data continues to reside within the same geography as its pair (except for Brazil South) for tax- and law-enforcement jurisdiction purposes.

> **Important**
>
>Most directions are paired in two directions, meaning they are the backup for the region that provides a backup for them (West US and East US back each other up). However, some regions, such as West India and Brazil South, are paired in only one direction. In a one-direction pairing, the Primary region does not provide backup for its secondary region. So, even though West India’s secondary region is South India, South India does not rely on West India. West India's secondary region is South India, but South India's secondary region is Central India. Brazil South is unique because it's paired with a region outside of its geography. Brazil South's secondary region is South Central US. The secondary region of South Central US isn't Brazil South.

### Sovereign Regions
In addition to regular regions, Azure also has sovereign regions. Sovereign regions are instances of Azure that are isolated from the main instance of Azure. You may need to use a sovereign region for compliance or legal purposes.

Azure sovereign regions include:

- US DoD Central, US Gov Virginia, US Gov Iowa and more: These regions are physical and logical network-isolated instances of Azure for U.S. government agencies and partners. These datacenters are operated by screened U.S. personnel and include additional compliance certifications.
- China East, China North, and more: These regions are available through a unique partnership between Microsoft and 21Vianet, whereby Microsoft doesn't directly maintain the datacenters.

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

### Use availability zones in your apps
You want to ensure your services and data are redundant so you can protect your information in case of failure. When you host your infrastructure, setting up your own redundancy requires that you create duplicate hardware environments. Azure can help make your app highly available through availability zones.

You can use availability zones to run mission-critical applications and build high-availability into your application architecture by co-locating your compute, storage, networking, and data resources within an availability zone and replicating in other availability zones. Keep in mind that there could be a cost to duplicating your services and transferring data between availability zones.

Availability zones are primarily for VMs, managed disks, load balancers, and SQL databases. Azure services that support availability zones fall into three categories:

- Zonal services: You pin the resource to a specific zone (for example, VMs, managed disks, IP addresses).
- Zone-redundant services: The platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).
- Non-regional services: Services are always available from Azure geographies and are resilient to zone-wide outages as well as region-wide outages.
Even with the additional resiliency that availability zones provide, it’s possible that an event could be so large that it impacts multiple availability zones in a single region. To provide even further resilience, Azure has Region Pairs.

## [Resource Groups](https://learn.microsoft.com/en-us/training/modules/describe-core-architectural-components-of-azure/6-describe-azure-management-infrastructure)
A resource is the basic building block of Azure. Anything you create, provision, deploy, etc. is a resource. Virtual Machines (VMs), virtual networks, databases, cognitive services, etc. are all considered resources within Azure.

![image](https://user-images.githubusercontent.com/48266482/223632841-96f5bdbc-38fa-4c9a-b55a-4d74cad01676.png)

Resource groups are simply groupings of resources. When you create a resource, you’re required to place it into a resource group. While a resource group can contain many resources, a single resource can only be in one resource group at a time. Some resources may be moved between resource groups, but when you move a resource to a new group, it will no longer be associated with the former group. Additionally, resource groups can't be nested, meaning you can’t put resource group B inside of resource group A.

Resource groups provide a convenient way to group resources together. When you apply an action to a resource group, that action will apply to all the resources within the resource group. If you delete a resource group, all the resources will be deleted. If you grant or deny access to a resource group, you’ve granted or denied access to all the resources within the resource group.

When you’re provisioning resources, it’s good to think about the resource group structure that best suits your needs.

For example, if you’re setting up a temporary dev environment, grouping all the resources together means you can deprovision all of the associated resources at once by deleting the resource group. If you’re provisioning compute resources that will need three different access schemas, it may be best to group resources based on the access schema, and then assign access at the resource group level.

There aren’t hard rules about how you use resource groups, so consider how to set up your resource groups to maximize their usefulness for you.

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



