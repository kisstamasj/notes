# Azure Architecture

## Regions 
A region is a set of datacenters deployed within a latency-defined perimeter and connected through a dedicated regional low-latency network

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
### Phisical Location
Each availability zone is a physical location within a region.

### Independent
Each zone has itsh own power, cooling and networking.

### Zones
Each region has a minimum of three zones.

![image](https://user-images.githubusercontent.com/48266482/219389259-6b108948-123b-4f73-a22d-e1a2e8a0efcd.png)

## Resource Groups
Every resource in Azure is in a Resource Group, there are no exceptions.

![image](https://user-images.githubusercontent.com/48266482/219393746-727782dd-047b-4653-8fdb-4ae8807d30a5.png)

The resource group is not a resource.

### One Resource
Each resource can only exist on a single resource group.

### Add/Remove
You can add ore remove resources to any resource group at any time.

### Move resource: 
You can move a resourece from one resource group to another.

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



